# kubectl-kubeplugin

`kubectl-kubeplugin` — це Bash‑плагін для `kubectl`, який виводить статистику використання CPU та памʼяті для Kubernetes‑ресурсів у форматі:

```
Resource, Namespace, Name, CPU, Memory
```

Плагін працює на основі `kubectl top`, тому вимагає встановленого **metrics‑server** у кластері.

---

## Встановлення

1. Клонувати репозиторій:

```bash
git clone https://github.com/kylib4444/scripts.git
cd scripts
```

2. Переконатися, що файл знаходиться за шляхом:

```
scripts/kubectl-kubeplugin
```

3. Зробити файл виконуваним:

```bash
chmod +x scripts/kubectl-kubeplugin
```

4. Додати директорію `scripts/` у PATH:

```bash
export PATH="$PATH:$(pwd)/scripts"
```

5. Перевірити, що kubectl бачить плагін:

```bash
kubectl plugin list
```

Очікуваний результат:

```
kubectl-kubeplugin
```

---

## Використання

### Загальний формат

```bash
kubectl kubeplugin <resource> -n <namespace>
```

### Приклади

Отримати статистику podʼів у namespace `kube-system`:

```bash
kubectl kubeplugin pods -n kube-system
```

Отримати статистику nodeʼів:

```bash
kubectl kubeplugin nodes
```

Отримати статистику podʼів у namespace `default`:

```bash
kubectl kubeplugin pods -n <namespace>
```

---

## Приклад реального виводу

```
Resource, Namespace, Name, CPU, Memory
pods, demo, ambassador-64d97bcfc9-b2vzp, 13m, 97Mi
pods, demo, cache-7995dc47c8-6xflh, 2m, 5Mi
pods, demo, db-57657d957c-nnbr2, 5m, 431Mi
pods, demo, demo-api-6cf9bb95-549mc, 2m, 4Mi
pods, demo, demo-ascii-7446d8b8b9-fvmfj, 1m, 5Mi
pods, demo, demo-data-64f785b878-bxrqj, 2m, 4Mi
pods, demo, demo-front-64b97cc6cf-2km55, 1m, 4Mi
pods, demo, demo-img-54868756dd-7gm44, 2m, 5Mi
pods, demo, demo-nats-0, 1m, 12Mi
pods, demo, demo-nats-box-58f884cff9-n5qq4, 1m, 0Mi
```

---

## 🛠 Вимоги

- Kubernetes cluster  
- Встановлений `metrics-server`  
- `kubectl` у PATH  
- Bash 4+  

---

## Структура репозиторію

```
scripts/
 └── kubectl-kubeplugin
README.md
```

---

## Ліцензія

Вільне використання в навчальних цілях.


## ⚠️ Примітка щодо назви файлу (`kubeplugin` vs `kubectl-kubeplugin`)

У репозиторії файл плагіна зберігається під назвою:

```
scripts/kubeplugin
```

Так вимагає умова завдання.

Однак система плагінів `kubectl` працює за іншим принципом:  
щоб команда

```
kubectl kubeplugin
```

запустила плагін, у `$PATH` має існувати файл з назвою:

```
kubectl-kubeplugin
```

Тобто `kubectl` автоматично виконує лише ті плагіни, чиї файли починаються з префікса `kubectl-`.

Через це для локального тестування необхідно створити копію:

```bash
cp scripts/kubeplugin scripts/kubectl-kubeplugin
```

Після цього плагін коректно викликається командою:

```bash
kubectl kubeplugin pods -n kube-system
```
