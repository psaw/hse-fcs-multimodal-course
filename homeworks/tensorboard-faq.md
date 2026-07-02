Для визуализации в TensorBoard замени `CSVLogger` на `TensorBoardLogger`:

### 1. Замени Logger в Trainer

В коде, где создаётся `Trainer`, замени:

```python
from pytorch_lightning.loggers import TensorBoardLogger

# Вместо CSVLogger используй TensorBoardLogger
logger = TensorBoardLogger("logs", name="vqa_baseline")

# Trainer остаётся тем же
trainer = pl.Trainer(
    max_epochs=10,
    accelerator="auto",
    devices="auto",
    callbacks=[checkpoint_callback, early_stop_callback],
    logger=logger,  # TensorBoardLogger вместо CSVLogger
    log_every_n_steps=50,
    val_check_interval=0.5,
    precision="16-mixed",
)
```

### 2. Запусти TensorBoard

После запуска обучения выполни в терминале (или в новой ячейке ноутбука):

```python
# В ноутбуке можно запустить TensorBoard так:
%load_ext tensorboard
%tensorboard --logdir logs/vqa_baseline
```

Или в отдельном терминале:

```bash
tensorboard --logdir logs/vqa_baseline
```

Затем открой в браузере адрес, который покажет TensorBoard (обычно `http://localhost:6006`).

### 3. Что будет видно в TensorBoard

- Scalars: `train_loss`, `train_acc`, `val_loss`, `val_acc` по эпохам/шагам
- Графики в реальном времени
- Возможность сравнивать разные запуски (если запускаешь несколько экспериментов)

### 4. Опционально: несколько экспериментов

Если хочешь сравнивать разные конфигурации, можно задать разные `name`:

```python
logger = TensorBoardLogger("logs", name="vqa_baseline_resnet18_frozen")
# или
logger = TensorBoardLogger("logs", name="vqa_baseline_resnet18_finetuned")
```

TensorBoard покажет их все в одном интерфейсе, можно будет переключаться между ними.

После замены `CSVLogger` на `TensorBoardLogger` и запуска обучения, логи будут писаться в `logs/vqa_baseline/version_X/`, и их можно будет просматривать в TensorBoard.





