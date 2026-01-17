<p align="center"><b>МОНУ НТУУ КПІ ім. Ігоря Сікорського ФПМ СПІСКС</b></p>
<p align="center">
<b>Звіт з лабораторної роботи 2</b><br/>
"Рекурсія"<br/>
дисципліни "Вступ до функціонального програмування"
</p>

<p align="right"><b>Студент</b>: Скібчик Арсен група КВ-21</p>
<p align="right"><b>Рік</b>: 2026</p>

## Загальне завдання
Реалізувати дві рекурсивні функції, що виконують дії з вхідними списками, згідно з варіантом.

### Вимоги до функцій:
1. Зміна списку має відбуватись за рахунок конструювання нового списку, а не зміни наявного.
2. Не допускається використання функцій вищого порядку чи стандартних функцій для роботи зі списками, що не наведені в четвертому розділі навчального посібника.
3. Реалізована функція не має бути функцією вищого порядку.
4. Не допускається використання псевдофункцій (деструктивного підходу).
5. Не допускається використання циклів.

## Варіант 2(17)

1. **Функція `remove-seconds-and-thirds`**: видаляє зі списку кожен другий і третій елементи.
2. **Функція `list-set-intersection`**: визначає перетин двох множин, заданих списками атомів.

## Завдання 1: Видалення кожного другого та третього елементів
```lisp
(defun remove-seconds-and-thirds (lst)
  (cond ((null lst) nil)
        (t (cons (car lst) 
                 (remove-seconds-and-thirds (cdddr lst))))))

```
## Завдання 2: Перетин двох множин
```lisp
(defun list-set-intersection (set1 set2)
  (cond ((null set1) nil)
        ;; Якщо перший елемент першої множини є в другій — додаємо його до результату
        ((member (car set1) set2)
         (cons (car set1) (list-set-intersection (cdr set1) set2)))
        ;; Якщо немає — просто переходимо до наступного елемента
        (t (list-set-intersection (cdr set1) set2))))
```
## Модульне тестування 
```Lisp
(defun check-task (name input expected-fn input-args expected)
  "Утиліта для перевірки результатів"
  (let ((result (apply expected-fn input-args)))
    (format t "~:[FAILED~;passed~]... ~a~%   Input: ~a~%   Expected: ~a~%   Result: ~a~%"
            (equal result expected) name input-args expected result)))

(defun test-lab2 ()
  (format t "--- Testing remove-seconds-and-thirds ---~%")
  (check-task "Test 1.1" nil #'remove-seconds-and-thirds '( (a b c d e f g) ) '(a d g))
  (check-task "Test 1.2" nil #'remove-seconds-and-thirds '( (1 2 3 4 5) ) '(1 4))
  (check-task "Test 1.3" nil #'remove-seconds-and-thirds '( nil ) nil)

  (format t "~%--- Testing list-set-intersection ---~%")
  (check-task "Test 2.1" nil #'list-set-intersection '( (1 2 3 4) (3 4 5 6) ) '(3 4))
  (check-task "Test 2.2" nil #'list-set-intersection '( (a b c) (x y z) ) nil)
  (check-task "Test 2.3" nil #'list-set-intersection '( (apple banana) (banana cherry) ) '(banana)))
```
(test-lab2)

