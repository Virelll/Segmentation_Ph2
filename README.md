# Segmentation_Ph2
______
## Описание данных
Датасет «Ph2» содержит дермоскопические изображения для исследования, сравнительного анализа и для классификации дермоскопических изображений меланомы. Он включает 80 распространенных невусов, 80 атипичных невусов и 40 меланом. Они представляют собой 8-битные цветные изображения RGB с разрешением 768x560 пикселей. https://www.dropbox.com/s/k88qukc20ljnbuo/PH2Dataset.rar
_____
## Задача
Реализовать и обучить модели UNet и SegNet с разными гиперпараметрами для задачи сегментации меланом на медицинских изображениях. Провести сравнительный анализ полученных результатов.

![Image alt](https://github.com/Virelll/Segmentation_Ph2/blob/main/dataset.png)

## Итог
Реализовано и обучено 7 моделей UNet и 8 моделей SegNet. 
### UNet

|  | epoches |	optimizator	| Loss_fnc	| lr	   | IoU |
|--| ------- |	-----------	| --------	| --	   | --- |
1|	30	|AdamW	|BCEWithLogitsLoss	    |0.0001	 |0.9215
2|	50	|AdamW	|BCEWithLogitsLoss	    |0.0001	 |0.9136
3|	75	|AdamW	|BCEWithLogitsLoss	    |0.0001  |0.9314
4|	50	|AdamW	|CrossEntropyLoss	      |0.0001	 |-
5|	50	|AdamW	|DiceLoss	              |0.00001 |0.9149
6|	50	|AdamW	|SoftBCEWithLogitsLoss	|0.00001 |0.9271
7|	50	|AdamW	|SoftBCEWithLogitsLoss	|0.0001  |0.9335

Можно сделать вывод, что CrossEntropyLoss не подходит для данной задачи и обучение модели не происходит. Обучение на количестве эпох больше 50 значительного улучшения итоговой метрики не дает. Наилучшее значение точности дала модель на восьмом обучении (количество эпох – 50, функция ошибки – SoftBCEWithLogitsLoss, оптимизатор – AdamW, шаг обучения 0,0001) равное 93,35%.

### SegNet

|  | epoches |	optimizator	| Loss_fnc	| lr	   | IoU |
|--| ------- |	-----------	| --------	| --	   | --- |
|1	|15	     |AdamW	|BCEWithLogitsLoss	|0.00001	|0.2745
|2	|15	     |AdamW	|BCEWithLogitsLoss	|0.0001	|0.3463
|3	|15	     |AdamW	|BCEWithLogitsLoss	|0.001	|0.2618
|4	|15	     |AdamW	|BCEWithLogitsLoss	|0.01	|0.3257
|5	|50      |AdamW	|DiceLoss	          |0.00001	|0.9138
|6	|10	     |AdamW	|DiceLoss	          |0.0001	|0.3218
|7	|50	     |AdamW	|SoftBCEWithLogitsLoss	|0.00001	|0.9369
|8	|50	     |AdamW	|SoftBCEWithLogitsLoss	|0.0001	|0.9509

После проведения нескольких экспериментов по обучению архитектуры SegNet, можно сделать вывод что для данной задачи и архитектуре SegNet не подходит loss функция BCEWithLogitsLoss, обучение не происходит. Для DiceLoss шаг обучения 0,0001 является большим и не дает обучаться модели. Лучше всего показала себя SoftBCEWithLogitsLoss на 50 эпохах при 0,00001 и 0,0001 на 93,69% и 95,09% соответсвенно.

Результат наилучшей модели:

![Image alt](https://github.com/Virelll/Segmentation_Ph2/blob/main/res1.png)
