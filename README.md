### Extrapolation_of_regression_of_complex_numbers

### Горшков Андрей Вячеславович
### Повышение точности экстраполяции регрессии для данных, содержащих комплексные числа, путем учета погрешности измерения переменных
------------------------------------------

Рассмотрена задача экстраполяции регрессии для наборов данных, содержащих **комплексные числа**, с практически абсолютной мультиколлинеарностью всех предикторов. Предполагается, что предикторы и целевая переменная заданы с некоторыми известными погрешностями измерений.

На сгенерированных наборах данных обучены различные модели из библиотеки scikit-learn, модели двухслойных нейронных сетей прямого распространения и модель регуляризации Тихонова [1], коэффициент регуляризации которой определяется по условию оптимизации нестандартной (для scikit-learn) метрики – обобщенной невязки, учитывающей информацию о погрешности измерения предикторов и целевой переменной (подробнее смотри репозиторий автора GorshkovAndrey / Extrapolation_of_regression). 

Необходимо отметить, что алгоритмы scikit-learn не поддерживают работу с **комплексными числами**, что не позволяет построить непосредственные модели регрессии для данных, содержащих **комплексные числа**, с помощью стандартных алгоритмов scikit-learn или нейронных сетей Keras. Для устранения этого препятствия автором разработан метод преобразования исходного датасета размером M×N с **комплексными числами** в датасет размером 2M×(2N-1) с **вещественными числами**, что позволяет использовать для построения достоверных моделей регрессии комплексных чисел стандартные алгоритмы scikit-learn или нейронные сети Keras (подробнее смотри репозиторий автора GorshkovAndrey / Regression_of_complex_numbers_using_Sklearn_and_Keras).

Несмотря на отличные метрики всех обученных моделей регрессоров из библиотеки Scikit-learn, результаты их прогнозов не только имеют неприемлемую точность, но и являются неустойчивыми – небольшие погрешности измерений данных приводят к недопустимым погрешностям прогноза целевой переменной (в терминологии ML это означает, что модели переобучаются). Максимальный модуль разброса (variance) осредненного прогноза различных моделей регрессоров достигает 24% при модуле смещения (bias) 18%.

При этом результаты прогнозов двухслойной нейронной сети прямого распространения являются достаточно устойчивыми и имеют приемлемую точность. Максимальный модуль разброса (variance) прогноза достигает 1,5% при модуле смещения (bias) 12%.

Наилучшие устойчивые прогнозы с приемлемой точностью выдает модель регуляризации Тихонова, учитывающая информацию о погрешности измерения предикторов и целевой переменной. Максимальный модуль разброса (variance) прогноза модели регуляризации Тихонова достигает 0,2% при модуле смещения (bias) 7%.

Выводы:
1. Алгоритмы Scikit-learn и Keras не поддерживают работу с **комплексными числами**, что не позволяет построить непосредственные модели регрессии для данных, содержащих **комплексные числа**, с помощью стандартных алгоритмов Scikit-learn или нейронных сетей Keras.
   
2. Разработан метод преобразования исходного датасета размером M×N с **комплексными числами** в датасет размером 2M×(2N-1) с **вещественными числами**, что позволяет использовать для построения достоверных моделей регрессии **комплексных чисел** стандартные алгоритмы Scikit-learn или нейронные сети Keras.

3. Игнорирование даже незначительной погрешности измерения значений предикторов и целевой переменной может привести к крайне большой погрешности прогноза экстраполяции регрессии (как для наборов данных, содержащих комплексные числа, так и для наборов данных, содержащих только вещественные числа).

4. Модели регрессоров Scikit-learn, обученные на наборах данных с мультиколлинеарными предикторами по условию оптимизации стандартных метрик Scikit-learn, могут привести к неустойчивым прогнозам экстраполяции с недопустимой погрешностью.

5. Для наборов данных с мультиколлинеарными предикторами для получения устойчивого прогноза экстраполяции с допустимой погрешностью следует использовать модель регуляризации Тихонова, учитывающую информацию о погрешности измерения предикторов и целевой переменной.

6. Для получения устойчивого прогноза экстраполяции с допустимой погрешностью при отсутствии информации о погрешности измерения предикторов и целевой переменной следует использовать модели нейронных сетей прямого распространения с подбором оптимального числа нейронов на каждом слое по условию оптимизации стандартных метрик Scikit-learn.

**Список литературы**
1. Тихонов А. Н., Гончарский А. В., Степанов В.В., Ягола А. Г. Регуляризирующие алгоритмы и априорная информация. – М.: Наука, 1983. – 200 с.
