from sys import stdin
from math import sqrt
 
max_x = -1e9
min_x = 1e9
max_y = -1e9
min_y = 1e9
for line in stdin:
    x1, y1, x2, y2 = map(int, line.split())
    max_x = max(max_x, max(x1, x2))
    max_y = max(max_y, max(y1, y2))
    min_x = min(min_x, min(x1, x2))
    min_y = min(min_y, min(y1, y2))
    # считаем середину отрезка
    mid_x = (x1 + x2) / 2
    mid_y = (y1 + y2) / 2
    # проверка случая когда отрезок выраждается в точку
    if mid_x != x1 or mid_y != y2:
        # находим половину расстояния отрезка
        s = sqrt((x1 - mid_x) ** 2 + (y1 - mid_y) ** 2)
       # нормируем вектор (x2 - mid_x, y2 - mid_y)
        xx1 = (x2 - mid_x) / s
        yy1 = (y2 - mid_y) / s
        #поварачиваем вектор на 90 градусов 
        rot_x = -yy1
        rot_y = +xx1     
        # возращаем длину отрезка и прибавляем к середине
        x3 = mid_x + rot_x * s
        y3 = mid_y + rot_y * s
        # пересчитываем координаты холста
        min_x = min(min_x, x3)
        min_y = min(min_y, y3)
        max_x = max(max_x, x3)
        max_y = max(max_y, y3)
# если не было входных данных, то считаем размер холста равный 0
if min_x == 10 ** 9:
    min_x = 0
    max_x = 0
    min_y = 0
    max_y = 0
print(max_x - min_x, max_y - min_y)
