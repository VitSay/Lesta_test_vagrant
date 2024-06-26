# Как запустить?🤔

```bash
cd dir/in/your/system
git clone <this_project_link>
cd Lesta_test_vagrant
run.cmd
```

>!!! **Перед запуском `run.cmd` В `Lesta_test_vagrant` надо создать папку `boxes` и загрузить туда [этот образ](https://app.vagrantup.com/ubuntu/boxes/jammy64)**

Далее надо подключиться к запущенной виртуальной машине:  

```bash
vagrant ssh
```

Vagrant сразу подключается к пользователю test и вы оказываетесь в домашнее директории пользователя test.

Далее можно сразу производить умножение матриц (все зависимости уже установлены и dll библиотека скомпилирована):

```bash
test@ubuntu-jammy:~$ python matrix_mul.py matrix1.txt matrix2.txt result.txt
```

В домашней директории test будут два файла с тестовыми матрицами matrix1.txt и matrix2.txt. В результате выполнения предыдущей команды в домашней директории появится файл result.txt. Если исходные матрицы не менялись, то результат в result.txt должен быть таким:

```txt
 -2100  4627 -4385 -1053 -2353 -1902 -3716 -1614  3073 -6402  1734  5220
 -2621  -658  -292 -3723 -9143 -1462   330  -787   812 -6692  1856  1943
  6003  -415  5261  2035  2196   933  2084 -1988 -5530  4270  1581 -1102
  4313  2613  1730  4160  1225   764  3071  3312 -1127   630 -1755 -3488
 -2027 -4117  1655 -1524   507  1020  2030 -1929 -4475  4656  -150 -1117
  2589  5116 -2741  3385  1766  1306 -1305 -3027 -1199  -524 -2620  -750
```

---

# Тестирование 📝

Тестирование реализовано с помощью pytest и tox. Достаточно написать команду:

```bash
test@ubuntu-jammy:~$ tox
```

Будут запущены pytest для двух версий python - 3.10 и 3.12.