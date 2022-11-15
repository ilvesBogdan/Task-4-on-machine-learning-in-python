## Введение в машинное обучение.

Выполнил студент группы 590-1<br/>Джумабаев Богдан

# Часть 1
```python
import numpy as np
from random import randint


def random_matrix(i: int, j: int, number_length: int) -> np.ndarray:
    """Создает матрицу заданного размера со случайными значениями.

    Аргументы:
    ----------
    * i, j -- размер матрицы
    * number_length -- количество знаков в каждом числе
    """
    if type(i) is int and type(j) is int and type(number_length) is int:
        degree_num = 10**number_length
        vfunc = np.vectorize(lambda x: int(x * degree_num))
        return vfunc(np.random.random((i, j)))

    raise Exception("В качестве аргументов возможны только целые числа.")


def question1(matrix_size: int) -> np.ndarray[int]:
    """Решение задания 1"""
    matrix = np.full((matrix_size, matrix_size), 1)
    i = j = int((matrix_size + 0.5) / 2)
    if matrix_size % 2:
        matrix[i][j] = 0
    return matrix


def question2(matrix_size: int) -> np.ndarray[int]:
    """Решение задания 2"""
    matrix = np.full((matrix_size, matrix_size), 0)
    for i in range(len(matrix)):
        j = i + 1
        if j >= matrix_size:
            break
        matrix[i][j] = j
    return matrix


def question3(matrix_size: int) -> np.ndarray[int]:
    """Решение задания 3"""
    matrix = random_matrix(matrix_size, matrix_size, 2)
    for line in matrix:
        average = sum(line) // len(line)
        yield line, average


def question4_1(arr: list[int]) -> list[int]:
    """Решение задания 4.1"""
    def func(x): return x * -1 if 3 < x and 8 > x else x
    return [func(i) for i in arr]


def question4_2(matrix: np.ndarray[int]) -> np.ndarray[int]:
    """Решение задания 4.2"""
    for i in range(len(matrix)):
        line = matrix[i]
        average = sum(line) // len(line)
        for j in range(len(line)):
            matrix[i][j] = line[j] - average
    return matrix


def question5(arr: np.array) -> np.array:
    """Решение задания 5"""
    new_arr = np.array(np.zeros(len(arr)*3-2))
    for i in range(len(arr)):
        new_arr[i*3] = arr[i]
    return new_arr


def question6(matrix: np.array) -> np.array:
    """Решение задания 6"""
    if (2 > len(matrix)):
        raise Exception("Требуется матрица с числом строк больше одной.")

    num_line1 = randint(0, len(matrix) - 1)
    num_line2 = randint(0, len(matrix) - 1)
    if num_line1 == num_line2:
        num_line2 -= 1
        if 0 > num_line2:
            num_line2 += 2
    temp_line = matrix[num_line1].copy()
    matrix[num_line1] = matrix[num_line2]
    matrix[num_line2] = temp_line
    return matrix


def question7(arr: list[object]) -> tuple[object, int]:
    """Решение задания 7"""
    unique = dict()
    for i in arr:
        if i in unique:
            unique[i] += 1
        else:
            unique.update({i: 1})
    return max(unique.items(), key=lambda i: i[1])


def question8(matrix: np.array) -> np.array:
    """Решение задания 8"""
    lenght = len(matrix)
    if 8 > lenght:
        raise Exception("Размер матрицы должен быть не меньше 8.")
    if len(matrix[0]) != lenght:
        raise Exception("Матрица должна быть квадратной.")
    if lenght % 4:
        raise Exception("Размер матрицы должен быть кратен 4.")

    step = lenght // 4
    arr = list()
    for s in range(0, lenght, step):
        temp = 0
        for i in range(0, step):
            i = s + i
            for j in range(0, step):
                j = s + j
                temp += matrix[i][j]
        arr.append(temp)
    return np.array([[arr[0], arr[1]], [arr[2], arr[3]]])


if __name__ == '__main__':
    print('\n Задание 1:', question1(3), sep='\n')
    print('\n Задание 2:', question2(5), sep='\n')
    print('\n Задание 3:', *question3(5), sep='\n')
    print('\n Задание 4.1:', question4_1(map(int, list('2347681266785683472'))), sep='\n')
    print('\n Задание 4.2:', question4_2(random_matrix(7, 5, 1)), sep='\n')
    print('\n Задание 5:', question5(np.array([1, 2, 3, 4, 5])))
    print('\n Задание 6:', question6(random_matrix(8, 5, 3)), sep='\n')
    print('\n Задание 7:', question7(list('12434546774983464')))
    print('\n Задание 8:', question8(random_matrix(16, 16, 1)), sep='\n')
```
