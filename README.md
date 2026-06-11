# WhatsApp superpack lib extractor (CI)

Извлекает распакованные нативные либы WhatsApp (`librtvip.so` и др.) из superpack,
запуская WhatsApp в **arm64 reDroid** на бесплатном GitHub arm64-раннере.

## Зачем
`libs.so` в APK — superpack-контейнер (zstd). Десктоп-распаковщика нет:
декомпрессия идёт только в Android-рантайме. Этот workflow и есть тот рантайм.

## Шаги

### 0. Авторизация (один раз)
```bash
gh auth login
```

### 1. Создать ПУБЛИЧНЫЙ репозиторий (нужен для бесплатных arm64-раннеров)
```bash
cd D:/PycharmProjectsD/wa-call-bridge/re/ci-extract
git init && git add .github && git commit -m "ci: WA superpack extractor"
gh repo create wa-superpack-extract --public --source=. --push
```

### 2. Залить APK-zip как release-ассет и получить URL
```bash
gh release create apks-v1 whatsapp-apks.zip -t "WA APKs" -n "split apks"
# URL ассета:
gh release view apks-v1 --json assets -q '.assets[0].url'
```
(71 МБ — в пределах лимита release-ассетов 2 ГБ.)

### 3. Запустить workflow
```bash
gh workflow run extract-wa-libs.yaml \
  -f apk_zip_url="<URL_из_шага_2>" \
  -f wait_seconds=150
gh run watch
```

### 4. Скачать результат
```bash
gh run download -n whatsapp-native-libs -D ../native/decompressed
```
→ ищем `librtvip.so` в `re/native/decompressed/`.

## Возможные итерации
- reDroid/binder на arm64-раннере может потребовать правок (модули ядра).
- Если WhatsApp падает на старте без GMS — декомпрессия всё равно обычно
  происходит в `Application.onCreate` до логина; увеличить `wait_seconds`.
- Проверить `so-inventory.txt` в артефакте — там список всех найденных `.so`.

## После извлечения
`librtvip.so` (arm64 ELF) → Ghidra → relay-allocation, SRTP-ключи, mlow.
