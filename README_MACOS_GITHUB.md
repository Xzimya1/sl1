# SleepGuard — автоматическая сборка DMG через GitHub Actions

## Что исправлено

Предыдущая версия workflow использовала `jurplel/install-qt-action`, и сборка остановилась внутри Python bootstrap этого action. В этой версии Qt устанавливается напрямую через Homebrew на GitHub macOS runner. Это убирает проблемный Python-шаг.

GitHub предоставляет macOS 15 ARM64 runner под меткой `macos-15` и Intel runner под `macos-15-intel`. Workflow собирает обе архитектуры отдельно.

## Запуск

1. Загрузите весь проект в GitHub repository.
2. Проверьте, что существует файл:

   `.github/workflows/build-macos-dmg.yml`

3. Откройте **Actions**.
4. Выберите **Build SleepGuard macOS DMG**.
5. Нажмите **Run workflow**.
6. Дождитесь зелёного статуса обоих jobs.
7. В разделе **Artifacts** скачайте:
   - `SleepGuard-macOS-arm64` для M1/M2/M3/M4/M5;
   - `SleepGuard-macOS-x86_64` для Intel Mac.

В архиве Artifact будет соответствующий `.dmg`.

## Если сборка снова красная

Откройте упавший job и пришлите скриншот или текст именно первой красной строки внутри шага, где произошла ошибка. Особенно полезны шаги `Install Qt 6 with Homebrew`, `Configure`, `Build` и `Create app and DMG`.

## Подпись Apple

DMG собирается без Apple Developer signing/notarization. Для локального использования этого достаточно, но Gatekeeper может показать предупреждение при первом запуске.
