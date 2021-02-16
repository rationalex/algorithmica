Пререквизиты: [Split-rebuild](Split-rebuild "wikilink")

## Split-merge

### Идея

В рамках структуры данных [split-rebuild](split-rebuild "wikilink") мы
регулярно перестраивали структуру данных. Оказывается, бывают
ситуации, когда перестраивать структуру данных не так выгодно,
как поддерживать ее в сбалансированном состоянии.

### Задача

Дан массив $a_n$, с которым надо выполнять следующие операции:

  - Вставка и удаление из произвольной позиции
  - Ответ на запрос "количество $x \\ge a$" на отрезке $\[l:r\]$
  - Массовые операции (например, переворот отрезка)

Заметим, что <st>это какая-то жесть</st> эту задачу мы уже могли решить
с помощью [split-rebuild](split-rebuild "wikilink"). Для этого нам надо
было бы хранить для каждого блока его отсортированную версию. Если для
каждого отсортированного элемента хранить его исходный индекс, то
можно будет делать \`split\`за линейное время. Таким образом, у нас
будет асимптотика $O(q \\sqrt{n} \\log n)$, ведь теперь для \`rebuild\`
и \`lower\\_bound\` нам понадобится сортировка.

### Склеиваем блоки

Теперь заметим, что мы можем склеить два соседних маленьких блока за
$O(K)$, где $K$ --- размер блока. Для этого нам понадобится стандартный
[merge](merge "wikilink"). Тогда будем склеивать блоки, если существует
пара соседних блоков, каждый из которых меньше, чем $\\frac{K}{2}$. А
резать блок будем, если его размер больше $2K$. Тогда блоков всегда
будет $O(\\frac{n}{K})$, а размер блоков будет $O(K)$.

### В чем выгода?

Теперь нам не надо будет делать сортировку. Для \`get\`-запросов
сложность осталась равной $O(q K \\log n)$, но теперь мы не
перестраиваем блоки, а склеиваем их за $O(\\frac{qn}{k})$. Тогда
при выборе $K = \\sqrt{\\log n}$ получаем сложность $O(q \\sqrt{n
\\log n})$.

[Категория:Конспекты](Категория:Конспекты "wikilink")