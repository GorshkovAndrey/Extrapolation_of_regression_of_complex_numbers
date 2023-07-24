### Extrapolation_of_regression_of_complex_numbers

### Горшков Андрей Вячеславович
### Повышение точности экстраполяции регрессии для данных, содержащих комплексные числа, путем учета погрешности измерения переменных и использованием стандартных регрессоров scikit-learn
------------------------------------------

Рассмотрена задача экстраполяции регрессии для наборов данных, содержащих комплексные числа, с практически абсолютной мультиколлинеарностью всех предикторов. Предполагается, что предикторы и целевая переменная заданы с некоторыми известными погрешностями измерений.

На сгенерированных наборах данных обучены различные модели регрессоров из библиотеки scikit-learn и модель регуляризации Тихонова, коэффициент регуляризации которой определяется по условию оптимизации нестандартной (для scikit-learn) метрики – обобщенной невязки, учитывающей информацию о погрешности измерения предикторов и целевой переменной. 

Необходимо отметить, что алгоритмы scikit-learn не поддерживают работу с комплексными числами, что не позволяет построить непосредственные модели регрессии для данных, содержащих комплексные числа, с помощью стандартных регрессоров scikit-learn. Для устранения этого препятствия автором разработан метод преобразования исходного датасета размером M×N с комплексными числами в датасет размером 2M×(2N-1) с вещественными числами, что позволило использовать для построения достоверных моделей регрессии комплексных чисел стандартные регрессоры scikit-learn.

Несмотря на отличные метрики (R2 ≈ 1) всех обученных моделей регрессоров из библиотеки scikit-learn, результаты их прогнозов не только имеют неприемлемую точность, но и являются неустойчивыми – небольшие погрешности измерений данных приводят к недопустимым погрешностям прогноза целевой переменной. При этом модель регуляризации Тихонова, учитывающая погрешности измерения предикторов и целевой переменной, выдает устойчивый прогноз с приемлемой точностью. Так в данной задаче погрешность осредненного прогноза различных моделей регрессоров из библиотеки scikit-learn составила от -8% до 33%, тогда как погрешность прогноза модели регуляризации Тихонова составила 7%.

Выводы:
1. Алгоритмы scikit-learn не поддерживают работу с комплексными числами, что не позволяет построить непосредственные модели регрессии для данных, содержащих комплексные числа, с помощью стандартных регрессоров scikit-learn.
 
2. Разработан метод преобразования исходного датасета размером M×N с комплексными числами в датасет размером 2M×(2N-1) с вещественными числами, что позволяет использовать для построения достоверных моделей регрессии комплексных чисел стандартные регрессоры scikit-learn.

3. Игнорирование даже незначительной погрешности измерения предикторов и целевой переменной может привести к крайне большой погрешности прогноза экстраполяции для наборов данных, содержащих комплексные числа.

4. Модели, обученные на наборах данных с мультиколлинеарными предикторами по условию оптимизации стандартных метрик из библиотеки scikit-learn, могут привести к неустойчивым прогнозам экстраполяции с недопустимой погрешностью.

5. Для моделей, обучаемых на наборах данных с мультиколлинеарными предикторами, для получения устойчивого прогноза экстраполяции с допустимой погрешностью следует использовать регуляризацию с учетом погрешности измерения предикторов и целевой переменной.
