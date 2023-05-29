в работе использовались

* pandas
* numpy

* matplotlib.pyplot

* nltk
* nltk.pos_tag
* nltk.corpus.wordnet
* nltk.stem.WordNetLemmatizer
* nltk.corpus.stopwords

* sklearn.feature_extraction.text.TfidfVectorizer
* sklearn.model_selection.train_test_split, RandomizedSearchCV
* sklearn.metrics.roc_auc_score, f1_score, roc_curve

* sklearn.linear_model.LogisticRegression
* sklearn.tree.DecisionTreeClassifier
* sklearn.dummy.DummyClassifier
* sklearn.pipeline.Pipeline

* imblearn.pipeline.make_pipeline
* imblearn.under_sampling.RandomUnderSampler
* imblearn.over_sampling.SMOTE

* lightgbm

### Итоги

Перед нами стояла задача: Обучить модель классифицировать комментарии на позитивные и негативные.

Цель: Обучить несколько моделей, выбрать лучшую, добиться значением метрики качества F1 не меньше 0.75. В нашем распоряжении набор данных с разметкой о токсичности правок.

Работы выполнили в 3 этапа

1. Загрузка и подготовка данных.
2. Обучение разных моделей.
3. Выбор модели и проверка на тестовых данных.

В ходе подготовки данных 
1. написали собственную функцию с помощью которой привели к строчным буквам все слова, убрали знаки пунктуации, удалили стоп слова, лемматизировали слова в тексте. 
2. обнаружили дисбаланс в целевом признаке примерно в соотношении 1:9 ![image.png](attachment:image.png)
3. разделили данные на тренировочную и тестовую выборки с сохранением дисбаланса классов.                                   

Для обучения выбрали модели 
* LogisticRegression 
* LGBMClassifier 
* DecisionTreeClassifier
Векторизацию данных выполнили при помощи TfidfVectorizer в make_pipeline.
Параметры моделей и TfidfVectorizer перебирали при помощи RandomizedSearchCV

Для работы с дисбалансом классов выбрали следующие методы:
1. Выполнили автоматическую балансировку классов при помощи 'class_weight': 'balanced'
2. Использовали функцию RandomUnderSampler для балансировки классов путем уменьшения мажоритарного класса
3. Выполнили балансировку классов путем увеличения меньшего класса с помощью функции SMOTE
4. Для проверки на адекватность использовали DummyClassifier, которая генерировала ответы соблюдая соотношение классов
 

Все модели отработали лучше чем DummyClassifier 

Получились примерно одинаковые значения F1 меры на моделях 
* LogisticRegression с автоматической балансировкой классов 
* LGBMClassifier с автоматической балансировкой классов
* LGBMClassifier балансировкой классов путем увеличения меньшего класса.

Все три модели переступили заданный рубеж 0,75 для F1. При этом модель LogisticRegression_class_weight_balanced показала результаты чуть лучше остальных трех и в метрике F1 и roc_auc. 

Модель LogisticRegression с автоматической балансировкой классов проверили на тестовой выборке с результатом 
* F1: 0.7759838546922301 
* AUC ROC: 0.8818215707119539

Метрика F1 превышает необходимый рубеж 0,75 заданный условием проекта.
Цели и задачи проекта выполнены.

Цели и задачи проекта выполнены.
