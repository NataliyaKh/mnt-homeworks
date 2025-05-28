# Домашнее задание к занятию 11 «Teamcity». Наталия Ханова. 

## Подготовка к выполнению

1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`.

![instances](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_vms.png)

4. Авторизуйте агент.

![auth](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_auth.png)

5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity).
6. Создайте VM (2CPU4RAM) и запустите [playbook](./infrastructure).

[playbook log](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/teamcity_playbook1.txt)

## Основная часть

1. Создайте новый проект в teamcity на основе fork.
2. Сделайте autodetect конфигурации.

![autodetect](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_2_autodetect.png)

3. Сохраните необходимые шаги, запустите первую сборку master.

![build2](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_3_build.png)

4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.

![steps](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_4_build_steps.png)

5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.

![settings](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_5_build_settings.png)

6. В pom.xml необходимо поменять ссылки на репозиторий и nexus.
7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.

![artefact](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_7_artefacts.png)

8. Мигрируйте `build configuration` в репозиторий.

![migr](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_8_repo.png)

![synchr](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_8_synchr.png)

9. Создайте отдельную ветку `feature/add_reply` в репозитории.

![branch](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_9_branch.png)

10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.

![Welcomer](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_10_welcomer.png)

11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.

![search](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_11_welcomerTest.png)

12. Сделайте push всех изменений в новую ветку репозитория.
13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.

![build13](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_13_build.png)

14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.

![merge](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_14_merge.png)

15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.

![noArt1](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_15_brF.png)

![noArt2](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_15_brM.png)

16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.

![jpom](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_16_jar_pom.png)

![jsettings](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_16_jar_settings.png)

![jsteps](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_16_jar_steps.png)

17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.

![rebuild](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_17_rebuild.png)

![artifacts](https://github.com/NataliyaKh/mnt-homeworks/blob/main/09-ci-05-teamcity/tc_17_artefacts.png)

18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
19. В ответе пришлите ссылку на репозиторий.

[example-teamcity](https://github.com/NataliyaKh/example-teamcity)

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
