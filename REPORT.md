## Laboratory work II

### Part I

1. **Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).**
2. **Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.**
   ```bash
   $ echo "# tp-lab02" >> README.md
   $ git init
   git add README.md
   git commit -m "first commit"
   git branch -M main
   git remote add origin https://github.com/nik-olay-93/tp-lab02.git
   git push -u origin main
   ```
3. **Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.**

   ```bash
   vim hello_world.cpp
   ```

   ```cpp
   #include <iostream>

   using namespace std;

   int main() {
   	cout << "Hello, World!" << endl;
   }
   ```

4. **Добавьте этот файл в локальную копию репозитория.**

   ```bash
   git add hello_world.cpp
   ```

5. **Закоммитьте изменения с _осмысленным_ сообщением.**

   ```bash
   git commit -m "Added hello_world.cpp"
   ```

6. **Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.**

   ```bash
   vim hello_world.cpp
   ```

   ```cpp
   #include <iostream>

   using namespace std;

   int main() {
   	string name;
   	cin >> name;
   	cout << "Hello world from " << name << endl;
   }
   ```

7. **Закоммитьте новую версию программы.**

   ```bash
   git add hello_world.cpp
   git commit -m "Changed hello_world.cpp"
   ```

8. **Почему не надо добавлять файл повторно `git add`?**
   ` -----`
9. **Запуште изменения в удалёный репозиторий.**

   ```bash
   git push origin main
   ```

10. **Проверьте, что история коммитов доступна в удалёный репозитории.**

![Коммиты](/images/commits.png)

### Part II

**Note:** _Работать продолжайте с теми же репоззиториями, что и в первой части задания._

1. **В локальной копии репозитория создайте локальную ветку `patch1`.**

   ```bash
   git checkout -b patch1
   ```

2. **Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.**

   ```bash
   vim hello_world.cpp
   ```

   ```cpp
   #include <iostream>

   int main() {
   	std::string name;
   	std::cin >> name;
   	std::cout << "Hello world from " << name << std::endl;
   }
   ```

3. **_commit_, _push_ локальную ветку в удалённый репозиторий.**

   ```bash
   git add hello_world.cpp
   git commit -m "Removed 'using namespace std;'"
   git push origin patch1
   ```

4. **Проверьте, что ветка `patch1` доступна в удалёный репозитории.**
   ![Ветки](/images/branches.png)
5. **Создайте pull-request `patch1 -> master`.**
6. **В локальной копии в ветке `patch1` добавьте в исходный код комментарии.**

   ```bash
   vim hello_world.cpp
   ```

   ```cpp
   #include <iostream>

   int main() {
   	std::string name;
   	// name input
   	std::cin >> name;
   	std::cout << "Hello world from " << name << std::endl;
   }
   ```

7. **commit**, **push**.

   ```bash
   git add hello_world.cpp
   git commit -m "Comment"
   git push origin patch1
   ```

8. **Проверьте, что новые изменения есть в созданном на _шаге 5_ pull-request**
   ![pull-request](/images/PR.png)

9. **удалённый репозитории выполните слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.**

10. **Локально выполните pull**.

    ```bash
    git switch main
    git pull origin main
    ```

11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.

    ```bash
    git log
    ```

12. Удалите локальную ветку `patch1`.

    ```bash
    git branch -D patch1
    ```

### Part III

**Note:** _Работать продолжайте с теми же репоззиториями, что и в первой части задания._

1. **Создайте новую локальную ветку `patch2`.**

   ```bash
   git checkout -b patch2
   ```

2. **Измените _code style_ с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.**

   ```bash
   clang-format -style=Mozilla hello_world.cpp
   ```

3. **commit**, **push**, создайте pull-request `patch2 -> master`.

   ```bash
   git add hello_world.cpp
   git commit -m "Formatted style"
   git push origin patch2
   ```

4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились _конфликтны_.
   ![Конфликт](/images/PR_con.png)
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.

   ```bash
   git pull origin main
   git rebase main
   ```

7. Сделайте _force push_ в ветку `patch2`

   ```bash
   git push --force origin patch2
   ```

8. Убедитель, что в pull-request пропали конфликтны.
9. Вмержите pull-request `patch2 -> master`.
