# lab3
#define_CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<locale.h>
#include<ctype.h>

#ifdef_WIN32
#include<windows.h>
#endif

structnode
{
charinf[256];
int priority;
structnode* next;
};

structnode* head = NULL;

// Функциядляочисткибуфераввода
voidclear_input_buffer() {
int c;
while ((c = getchar()) != '\n'&& c != EOF);
}

// Функция для безопасного ввода строки с пробелами
voidsafe_input_string(char* buffer, intsize) {
if (fgets(buffer, size, stdin) != NULL) {
// Удаляемсимволновойстроки
buffer[strcspn(buffer, "\n")] = 0;
}
}

// Функция для безопасного ввода числа
intsafe_input_int() {
charinput[100];
int number;

while (1) {
if (fgets(input, sizeof(input), stdin) != NULL) {
// Пытаемся преобразовать в число
if (sscanf(input, "%d", &number) == 1) {
return number;
            }
            printf("Ошибка! Введитецелоечисло: ");
}
    }
}

structnode* get_struct(void)
{
structnode* p = NULL;
chars[256];
intprio;

if ((p = (structnode*)malloc(sizeof(structnode))) == NULL)
{
printf("Ошибка при распределении памяти\n");
exit(1);
    }

printf("Введитеназваниеобъекта: ");
safe_input_string(s, sizeof(s));

printf("Введите приоритет объекта: ");
prio = safe_input_int();

if (strlen(s) == 0)
    {
printf("Запись не была произведена\n");
free(p);
returnNULL;
    }

strcpy(p->inf, s);
    p->priority = prio;
    p->next = NULL;

return p;
}

voidspstore(void)
{
structnode* p = get_struct();
if (p == NULL) return;

if (head == NULL || p->priority > head->priority)
    {
        p->next = head;
        head = p;
return;
    }

structnode* current = head;
while (current->next != NULL&& current->next->priority >= p->priority)
    {
        current = current->next;
    }

    p->next = current->next;
    current->next = p;
}

void review(void)
{
structnode* struc = head;
if (head == NULL)
{
printf("Список задач пуст\n");
return;
    }

printf("\nЗадачи\n");
int count = 1;
while (struc)
    {
printf("%d. Имя: %s, Приоритет: %d\n", count, struc->inf, struc->priority);
struc = struc->next;
        count++;
    }
}

voidfree_list(void)
{
structnode* current = head;
structnode* next;

while (current != NULL)
    {
        next = current->next;
        free(current);
        current = next;
    }
    head = NULL;
}

void menu(void)
{
int choice;

while (1)
    {
printf("\nПРИОРИТЕТНАЯОЧЕРЕДЬ\n");
printf("1. Добавить элемент\n");
printf("2. Просмотреть очередь\n");
printf("3. Выход\n");
printf("Выберите действие: ");

// Безопасный ввод выбора меню
charinput[100];
if (fgets(input, sizeof(input), stdin) != NULL) {
// Проверяем, что введено одно число
if (sscanf(input, "%d", &choice) == 1) {
if (choice >= 1 && choice <= 3) {
switch (choice)
                    {
case 1:
spstore();
break;
case 2:
review();
break;
case 3:
                        free_list();
printf("Вывышлиизпрограммы\n");
return;
}
                }
else {
printf("Ошибка! Введите число от 1 до 3.\n");
                }
            }
else {
printf("Ошибка! Введите число от 1 до 3.\n");
}
        }
    }
}

int main(void)
{
#ifdef_WIN32
SetConsoleCP(1251);
SetConsoleOutputCP(1251);
#endif

setlocale(LC_ALL, "Russian");
menu();



#define_CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<locale.h>

#ifdef_WIN32
#include<windows.h>
#endif

structnode
{
charinf[256];
structnode* next;
};

structnode* front = NULL; // началоочереди
structnode* rear = NULL;  // конецочереди

voidclear_input_buffer() {
int c;
while ((c = getchar()) != '\n'&& c != EOF);
}

voidsafe_input_string(char* buffer, intsize) {
if (fgets(buffer, size, stdin) != NULL) {
buffer[strcspn(buffer, "\n")] = 0;
    }
}


intsafe_input_int() {
charinput[100];
int number;

while (1) {
if (fgets(input, sizeof(input), stdin) != NULL) {
if (sscanf(input, "%d", &number) == 1) {
return number;
            }
printf("Ошибка! Введитецелоечисло: ");
        }
    }
}


structnode* get_struct(void)
{
structnode* p = NULL;
chars[256];

if ((p = (structnode*)malloc(sizeof(structnode))) == NULL)
{
printf("Ошибка при распределении памяти\n");
exit(1);
    }

printf("Введитеданныеэлемента: ");
safe_input_string(s, sizeof(s));

if (strlen(s) == 0)
    {
printf("Запись не была произведена\n");
free(p);
returnNULL;
    }

strcpy(p->inf, s);
    p->next = NULL;

return p;
}

void enqueue(void)
{
structnode* p = get_struct();
if (p == NULL) return;

if (rear == NULL) 
    {
        front = p;
        rear = p;
    }
else
    {
        rear->next = p;
        rear = p;
}
printf("Элемент '%s' добавлен в очередь!\n", p->inf);
}


void dequeue(void)
{
if (front == NULL)
    {
printf("Очередьпуста!\n");
return;
    }

structnode* temp = front;
printf("Элемент '%s' удален из очереди!\n", front->inf);

front = front->next;


if (front == NULL)
    {
        rear = NULL;
    }

    free(temp);
}


voiddisplay_queue(void)
{
structnode* current = front;
if (front == NULL)
    {
printf("Очередьпуста\n");
return;
    }

printf("\nСодержимоеочереди\n");
int count = 1;
while (current)
    {
printf("%d. %s\n", count, current->inf);
        current = current->next;
        count++;
    }
}


voidfree_queue(void)
{
structnode* current = front;
structnode* next;

while (current != NULL)
    {
        next = current->next;
        free(current);
        current = next;
    }
    front = NULL;
    rear = NULL;
}

void menu(void)
{
int choice;

while (1)
    {
printf("\nСТРУКТУРАДАННЫХ 'ОЧЕРЕДЬ'\n");
printf("1. Добавить элемент\n");
printf("2. Удалить элемент\n");
printf("3. Просмотреть очередь\n");
printf("4. Выход\n");
printf("Выберите действие: ");

charinput[100];
if (fgets(input, sizeof(input), stdin) != NULL) {
if (sscanf(input, "%d", &choice) == 1) {
if (choice >= 1 && choice <= 4) {
switch (choice)
{
case 1:
enqueue();
break;
case 2:
dequeue();
break;
case 3:
display_queue();
break;
case 4:
free_queue();
printf("Выход из программы. Память очищена.\n");
return;
                    }
                }
else {
printf("Ошибка! Введите число от 1 до 4.\n");
                }
            }
else {
printf("Ошибка! Введите число от 1 до 4.\n");
}
        }
    }
}

int main(void)
{
#ifdef_WIN32
SetConsoleCP(1251);
SetConsoleOutputCP(1251);
#endif

setlocale(LC_ALL, "Russian");
menu();

return 0;
}







#define_CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<locale.h>
#include<windows.h>


structnode
{
charinf[256];        
structnode* next;   
};

structnode* head = NULL;

voidset_console_russian()
{
SetConsoleCP(1251); 
SetConsoleOutputCP(1251);
setlocale(LC_ALL, "Russian");
}

voidclear_input_buffer()
{
int c;
while ((c = getchar()) != '\n'&& c != EOF);
}

structnode* get_struct(void)
{
structnode* p = NULL;
chars[256];

if ((p = (structnode*)malloc(sizeof(structnode))) == NULL)
{
printf("Ошибка при распределении памяти\n");
exit(1);
    }

printf("Введитеназваниеобъекта: ");

if (fgets(s, sizeof(s), stdin) == NULL) {
printf("Ошибкаввода\n");
        free(p);
returnNULL;
    }

size_tlen = strlen(s);
if (len> 0 &&s[len - 1] == '\n') {
s[len - 1] = '\0';
    }

if (strlen(s) == 0)
{
printf("Запись не была произведена\n");
free(p);
returnNULL;
    }

strcpy(p->inf, s);
    p->next = NULL;

return p; 
}


voidspstore(void)
{
structnode* p = NULL;
    p = get_struct();

if (p != NULL)
    {
        p->next = head;
        head = p;
printf("Элемент '%s' добавлен в стек\n", p->inf);
}
}


void review(void)
{
structnode* struc = head;

if (head == NULL)
    {
printf("Стекпуст\n");
return;
}

printf("Содержимое стека (от вершины к основанию):\n");
while (struc)
    {
printf("Имя - %s\n", struc->inf);
struc = struc->next;
    }
}


voiddel_stack(void)
{
if (head == NULL)
    {
printf("Стекпуст\n");
return;
    }

structnode* temp = head;
printf("Удаленэлемент: %s\n", temp->inf);
    head = head->next;    
    free(temp);           
}


voidfind_element(void)
{
charsearch_name[256];

if (head == NULL)
    {
printf("Стекпуст\n");
return;
}

printf("Введите имя для поиска: ");

if (fgets(search_name, sizeof(search_name), stdin) == NULL) {
printf("Ошибкаввода\n");
return;
    }

size_tlen = strlen(search_name);
if (len> 0 &&search_name[len - 1] == '\n') {
search_name[len - 1] = '\0';
    }

structnode* struc = head;
int found = 0;

while (struc)
    {
if (strcmp(search_name, struc->inf) == 0)
        {
printf("Элементнайден: %s\n", struc->inf);
            found = 1;
break;
        }
struc = struc->next;
}

if(!found)
    {
printf("Элемент не найден\n");
}
}

intmain()
{
set_console_russian(); 

int choice;

do {
printf("\nМенюоперацийсостеком:\n");
printf("1 - Добавитьэлемент\n");
printf("2 - Просмотреть стек\n");
printf("3 - Удалить элемент из стека\n");
printf("4 - Поиск элемента\n");
printf("5 - Выход\n");
printf("Выберитедействие: ");

if (scanf("%d", &choice) != 1) {
printf("Ошибкаввода!\n");
clear_input_buffer();
continue;
        }
clear_input_buffer();

switch (choice) {
case 1:
spstore();
break;
case 2:
review();
break;
case 3:
del_stack();
break;
case 4:
find_element();
break;
case 5:
printf("Выход из программы\n");
break;
default:
printf("Неверный выбор! Попробуйте снова.\n");
        }
    } while (choice != 5);

// Освобождение памяти перед выходом
while (head != NULL)
    {
structnode* temp = head;
        head = head->next;
        free(temp);
}

return 0;
}

return 0;
}
