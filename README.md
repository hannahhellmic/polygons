# Геометрические преобразования и анализ многоугольников

Этот Jupyter Notebook содержит функции для генерации, визуализации, трансформации и анализа двумерных многоугольников, таких как прямоугольники, треугольники и шестиугольники. Основной акцент сделан на изучении геометрических преобразований и фильтрации фигур по различным признакам.

## Содержание

### 📐 Генерация фигур
- `gen_rectangle`, `gen_triangle`, `gen_hexagon` — генераторы многоугольников с заданными параметрами (ширина, высота, отступы и т.д.)
- `get_figures` — получение N фигур из генератора

### 🎨 Визуализация
- `visualize_polygons(*polygons)` — отрисовка фигур с использованием matplotlib

### 🔁 Геометрические преобразования
- `tr_translate(dx, dy)` — параллельный перенос
- `tr_rotate(angle, center)` — поворот вокруг точки
- `tr_symmetry(axis)` — симметрия относительно оси X или Y
- `tr_homothety(k, center)` — гомотетия (масштабирование)
- `tr_homothety_increasing_element` — прогрессивное масштабирование

### 📊 Метрики и анализ
- `polygon_area(polygon)` — площадь
- `perimeter(polygon)` — периметр
- `min_side_length(polygon)` — минимальная длина стороны
- `is_convex(polygon)` — проверка на выпуклость
- `point_in_convex_polygon(point, polygon)` — проверка попадания точки внутрь выпуклого многоугольника

### 🔍 Фильтрация и поиск
- `flt_convex_polygon` — только выпуклые
- `flt_angle_point(point)` — содержит вершину в заданной точке
- `flt_square(max_area)` — с площадью меньше заданной
- `flt_short_side(max_length)` — с короткой стороной
- `flt_point_inside(point)` — содержащие точку внутри
- `flt_polygon_angles_inside(target_polygon)` — содержащие хотя бы одну вершину другой фигуры
- `agr_origin_nearest` - поиск угла, самого близкого к началу координат
- `agr_max_side` - поиск самого длинной стороны многоугольника
- `agr_min_area` - поиск самой маленькой площади многоугольника
- `agr_perimeter` - расчет суммарного периметра
- `agr_area` - расчет суммарной площади

## Использование

Генерация фигур (итератор):
```python
  rectangles = gen_rectangle(width=2, height=1)
```

Генерация конкретного количества фигур:
```python
  rectangles = get_figures(gen_rectangle(width=2, height=1), amount=5)
```

Визуализация полигонов (передаются списки):
```python
  visualize_polygons(p1, p2, p3)
```

Применение функций трансформаторов при помощи функции `map`:
```python
  triangles = get_figures(gen_triangle(width=2, height=4), amount=7)
  triangles_transformed = list(map(tr_rotate(30), map(tr_translate(dy=3), triangles)))
```

Применение фильтрации при помощи функции `filter`:
```python
  filtered_polygons = filter(flt_short_side(2.3), polygons)
```

Поиск полигонов при помощи функции `reduce`:
```python
  min_area_poly = reduce(agr_min_area, polygons)
```

Поиск суммарных величин при помощи функции `reduce`:
```python
  total_area = reduce(agr_area, polygons, 0)
```

Применение декораторов:
```python
  @translate_decorator(dx=2, dy=3)
  @rotate_decorator(angle_degrees=90, center=(0, 0))
  @homothety_decorator(scale_factor=2, center=(0, 0))
  def create_triangle():
      return [(0, 0), (1, 0), (0, 1)]
```
