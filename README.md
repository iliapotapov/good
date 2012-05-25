good
====

#include "stdafx.h"
#include <stdio.h>
#include <conio.h>
#include <iostream>
#include <fstream>
#include <string>
#include <sstream>
#include <time.h>
using namespace std;

struct Node { // структура элемента списка
  string name;
	int key;
	Node *next;
};

class List {
private: Node*first;
		 Node*tail;
public: void Print();
		void Print_list();
		void AddFront(string name, int key);
		void AddBack(string name, int key);
		void AddAuto(int count);
		void Init();
		bool DelBack();
		bool DelBegin();
		bool DelAll();
		void Upload();
		void Unload();
		void Edit_End();
		void Edit_Average();
		void Menu();
};

void List::Init() {
	first=NULL;
	tail=NULL;
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

void List::AddFront(string name, int key){
	Node* list=new Node;
	if (first==NULL) {
		list->next=NULL;
		first=list;
		tail=list;
		tail=first;
	}
	else {
		list->next=first;
		first=list;
	}
	list->name=name;
	list->key=key;
}

void List::AddBack(string name, int key) {
	Node* list=new Node;
	list->next=NULL;
	if (!first) {
		first=list;
		tail=list;
		tail=first;
	}
	else {
		tail->next=list;
		tail=list;
	}
	list->name=name;
	list->key=key;
}

void List::AddAuto(int count) {
	srand(time(NULL)); 

	int* arr=new int[99];
	for (int i=0;i<100;i++)
		arr[i]=0;

	for (int i=0;i<count;i++) {
		Node* list=new Node;
		string name="Element";

		int id;
		bool T=true;
		while (1) {
			T=true;
			id=1+(int)rand()%100; 
		
			for (int k=0;k<100;k++) {
				if (id==arr[k]) {
					T=false;
					break;
				}
			}
			
			if (T==true) {
				arr[i]=id;
				break;
			}
		}
		
		stringstream temp;
		temp << id;
        string iden;
	    temp >> iden;

		list->next=NULL;
		if (!first) {
			first=list;
			tail=list;
		}
		else {
			tail->next=list;
			tail=list;
		}

		list->name=name+iden;	
		list->key=id;
	}
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

bool List::DelBack () {
	if (!first) {
		setlocale(LC_ALL,".1251");
		cout << "В списке 0 элементов\n";
		cout << "Нажмите \"R\" для возврата:\n";
		char t;
		do {
			cin >> t;
		}
		while (t!='R'&&t!='r');

		switch (t)
		{ case 'R':
			system("cls");
			break;
		}
		return false;
	}
	
	Node* list=first;
	Node* temp=first;

	if (tail==first) {
		first=NULL;
		tail=NULL;
		free(list);
		setlocale(LC_ALL,".1251");
		cout << "В списке 0 элементов";
		getch();
		return true; 
	}
	
	else {
		while (temp->next->next) 
			temp=temp->next;
		temp->next=NULL;
	    delete tail;
		tail=temp;
        return true;
	}
}

bool List::DelBegin () {
	if (!first) {
		setlocale(LC_ALL,".1251");
		cout << "В списке 0 элементов\n";
		cout << "Нажмите \"R\" для возврата:\n";
		char t;
		do {
			cin >> t;
		}
		while (t!='R'&&t!='r');

		switch (t)
		{ case 'R':
			system("cls");
			break;
		}
		return false;
	}

	else {
		Node* list=first;

		if (list->next==NULL) {
			first=NULL;
			tail=NULL;
			delete list;
			setlocale(LC_ALL,".1251");
			cout << "В списке 0 элементов";
			getch();
			return true; 
		}
	
		else {
			first=list->next;
			delete list;
			list=first;
			return true;
		}
	}
}

bool List::DelAll() {
	if (!first) {
		setlocale(LC_ALL,".1251");
		cout << "В списке 0 элементов. Удаление невозможно\n";
		cout << "Нажмите \"R\" для возврата:\n";
		char t;
		do {
			cin >> t;
		}
		while (t!='R'&&t!='r');

		switch (t)
		{ case 'R':
			system("cls");
			break;
		}
		return false;
	}
	else {
		Node* list=first;
	Node* temp=new Node;

		while (list) {
			temp = list;
			list = list->next;
			first=list;
			first=NULL;
			delete temp;	
		}
		tail=NULL;
		setlocale(LC_ALL,".1251");
		return true;
	}
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

void List::Print() {
	setlocale(LC_ALL,".1251");
	if (first!=NULL) {
		cout << "--------------------------------------------------------------------------------" << endl;
		cout << "|    № п/п    |    Ключевой признак    |              Информация               |" << endl;
		cout << "--------------------------------------------------------------------------------" << endl;
		setlocale(LC_ALL,".866");
	
		Node* list=first;

		int i=0;
		while (list) { 
				i++;
			cout << "|     " << i;
			if (i<10)
				cout << " ";
			cout << "      |";

			cout << "           " << list->key;
			if (list->key<10)
				cout << " ";
			cout << "           |"; 

			string temp=list->name;
			string space=" ";
			int count=0;
			while (temp.size()<35) {
						temp=temp+space;
						count++;
			}
			cout << "    " << list->name; 
			for (int i=0;i<count;i++)
				cout << " ";
			cout << "|" << endl;

			list=list->next;
		}

		cout << "--------------------------------------------------------------------------------" << endl;
		setlocale(LC_ALL,".1251");

		list=first;
	}
	else 
		cout << "В списке 0 элементов. Просмотр недоступен\n";
}

void List::Print_list() {
	if (first!=NULL) {
		int key;

		Node* list=first;
		do {
			setlocale(LC_ALL,".1251");
			cout << "Нажмите \"ПРОБЕЛ\" для возврата:\n\n";
			
			setlocale(LC_ALL,".866"); // чтобы из списка выводилось на русском (кодировка DOS)
			cout << " >> " << list->key << ". " << list->name << "\n"; // вывод полей текущего элемента списка
	    	
			key=getch();
			if (key==227) // считывание нажатой клавиши
				getch();
			system("cls"); // очистка экрана

			switch(key) {
				case 77: // кнопка 'вправо'
					if(list->next!=NULL)
						list = list->next;
					break;
			}
			setlocale(LC_ALL,".1251");
		}
		while( key!=32); // пока не нажат пробел
	}
	else {
		setlocale(LC_ALL,".1251");
		cout << "В списке 0 элементов. Просмотр недоступен\n";
		cout << "Нажмите \"R\" для возврата:\n";
		char t;
		do {
			cin >> t;
		}
		while (t!='R'&&t!='r');

		switch (t)
		{ case 'R':
			system("cls");
			break;
		}
	}
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

void List::Upload(void) {
	if (first!=NULL) {
		Node* list=new Node;
		list=first;
		int count=0;

		while(list) {
			count++;
			list=list->next;
		}
		list=first;

		Node*b=new Node[50];

		for (int i=0;i<count;i++) {
			b[i].name=list->name;
			b[i].key=list->key;
			list=list->next;
		}

		FILE*f;
		f=fopen("list_file.txt","w");
		fclose(f);
		f=fopen("list_file.txt","a");
		fwrite(&count,sizeof(int),1,f);
		for (int i=0;i<count;i++) {
			fwrite(&b[i],sizeof(Node),1,f);
		}

		fclose(f);
	}
	else {
		setlocale(LC_ALL,".1251");
		cout << "В списке 0 элементов. Загрузка в файл невозможна\n";
		cout << "Нажмите \"R\" для возврата:\n";
		char t;
		do {
			cin >> t;
		}
		while (t!='R'&&t!='r');

		switch (t){ 
			case 'R':
				system("cls");					
				break;
		}
	}
}

void List::Unload() {
	FILE *fp;
	fp=fopen("list_file.txt","r");

	if (fp!=NULL) {
		system("cls");
		int count;

		Node* temp1=new Node;
		if (first!=NULL) {
			Node* tmp;
			temp1=first;

			while(temp1) {
				tmp = temp1;
				temp1 = temp1->next;
				free(tmp);
			}
			free(temp1);
			temp1=NULL;
			first=NULL;
		}

		Node*b=new Node[50];
		Node* list=new Node;
		FILE*f;
		f=fopen("list_file.txt","r");
		fread(&count,sizeof(int),1,f);

		if (!first) {
			list->next=NULL;
			first=list;
			tail=list;
		
			fread(&b[0],sizeof(Node),1,f);
			list->name=b[0].name;
			list->key=b[0].key;
		}

			for (int i=1;i<count;i++) {
				list=tail;

				fread(&b[i],sizeof(Node),1,f);

				Node* temp=new Node;
				temp->name=b[i].name;
				temp->key=b[i].key;

				temp->next=NULL;
				list->next=temp;
				tail=temp;
			}
		list=first;

		fclose(f);
	}
	else {
		setlocale(LC_ALL,".1251");
		cout << "Файл не существует. Выгрузка невозможна\n";
		cout << "Нажмите \"R\" для возврата:\n";
		char t;
		do {
			cin >> t;
		}
		while (t!='R'&&t!='r');

		switch (t)
		{ case 'R':
			system("cls");
			break;
		}
	}
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

void List::Edit_End() {
	if (first!=NULL) {
		string name;
		int error;
		int key;

		do
		{
			cout << "Введите ключ элемента: ";
			error = 0;
			cin >> key;
			if( cin.fail() ) // если ошибка при вводе
			{
				cout << "Количество указано неверно, должно быть число\n";
				error = 1;
			}
			cin.clear(); fflush(stdin); // очистка буфера ввода
		}
		while(error == 1);

		cout << "Введите название элемента: ";
		cin.sync();
		getline(cin,name);
		cin.clear(); fflush(stdin); // очистка буфера ввода

		Node* list=first;

		while(list->next) 
			list=list->next;

		list->name=name;
		list->key=key;
	}
	else {
		cout << "Список пуст. Редактирование невозможно\n";
		cout << "Нажмите \"R\" для возврата:\n";
		char t;
		do {
			cin >> t;
		}
		while (t!='R'&&t!='r');

		switch (t)
		{ case 'R':
			system("cls");
			break;
		}
	}
}

void List::Edit_Average() {
	if (first!=NULL) {
		string name;
		int error;
		int key;

		do
		{
			cout << "Введите ключ элемента: ";
			error = 0;
			cin >> key;
			if( cin.fail() ) // если ошибка при вводе
			{
				cout << "Количество указано неверно, должно быть число\n";
				error = 1;
			}
			cin.clear(); fflush(stdin); // очистка буфера ввода
		}
		while(error == 1);
		
		cout << "Введите название элемента: ";
		cin.sync();
		getline(cin, name);
		cin.clear(); fflush(stdin); // очистка буфера ввода
				
		Node* list=first;

		int count=1;
		while(list->next) {
			count++;
			list=list->next;
		}
		list=first;

		int temp;
		temp=count%2;

		if (temp!=0) {
			count =(count+1) / 2;

			for (int i=0; i<count-1;i++) 
				list=list->next;

			list->name=name;
			list->key=key;
		}
		else {
			count=count/2;

			setlocale(LC_ALL,".1251");
			cout << "Число элементов четное. Нажмите 1 или 2, чтобы выбрать левый или правый средний:\n";
			setlocale(LC_ALL,".866");

			int pos;
			do
				cin >> pos;
			while (pos!=1&&pos!=2);
		
			if (pos==1) {
				for (int i=0; i<count-1;i++) 
					list=list->next;

				list->name=name;
				list->key=key;
			}
			if (pos==2) {
				for (int i=0; i<count;i++) 
					list=list->next;

				list->name=name;
				list->key=key;
			}
		}
		setlocale(LC_ALL,".1251");
		list=first;
	}
	else {
		cout << "Список пуст. Редактирование невозможно\n";
		cout << "Нажмите \"R\" для возврата:\n";
		char t;
		do {
			cin >> t;
		}
		while (t!='R'&&t!='r');

		switch (t)
		{ case 'R':
			system("cls");
			break;
		}
	}
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

void List::Menu(){

	struct Menu	{
		string r;
		string B[5];
	};
	
	List p1;
	p1.Init();
	int error;
	Node tmp;

	setlocale(LC_ALL,".1251");
	Menu item[6]; 
	int N=6;
	int M=4;
	int U=3;
	int position_m=1;
	int position_pm=1;

	item[0].r ="Добавление элементов в список  ";
	item[1].r ="Удаление элементов из списка   ";
	item[2].r ="Редактирование элементов списка";
	item[3].r ="Просмотр списка                ";
	item[4].r ="Работа с файлом                ";
	item[5].r ="Выход из программы             ";

	for (int i=0;i<N-1;i++)
		if (position_m==i+1)
			cout << "* " << i+1 << "." <<  item[i].r << " *\n";
		else 
			cout << "  " << i+1 << "." << item[i].r << " \n";

	if (position_m==6)
		cout << "* " << 0 << "." << item[5].r<< " *\n";
	else 
		cout << "  " << 0 << "." << item[5].r << " \n";

	item [0].B[0]="Начало                  ";
	item [0].B[1]="Конец                   ";
	item [0].B[2]="Автоматически(генератор)";
	item [0].B[3]="Назад                   ";

	item [1].B[0]="Начало";
	item [1].B[1]="Конец ";
	item [1].B[2]="Полное";
	item [1].B[3]="Назад ";

	item [2].B[0]="Средний  ";
	item [2].B[1]="Последний";
	item [2].B[2]="Назад    ";

	item [3].B[0]="Таблица  ";
	item [3].B[1]="Прокрутка";
	item [3].B[2]="Назад    ";

	item [4].B[0]="Сохранение списка в файл";
	item [4].B[1]="Выгрузка списка из файла";
	item [4].B[2]="Назад                   ";

	item [5].B[0]="Вернуться";
	item [5].B[1]="Да       ";

	bool Q=true;

	int v,w,x,y,z;
	while (1)	{
		x=getch();
		if (x==224) 
			x=getch();
		switch (x) {
		case 49:
			position_m=1;
			break;
		case 50: 
			position_m=2;
			break;
		case 51: 
			position_m=3;
			break;
		case 52: 
			position_m=4;
			break;
		case 53: 
			position_m=5;
			break;
		case 54: 
			position_m=6;
			break;
		case 48: 
			position_m=6;
			break;
		case 80:
			position_m++;
			break;
		case 72:
			position_m--;
			break;
		case 13:
			Q=false;
			break;
		case 27:
			position_m=6;
			Q=false;
			break;
		default:
			break;
		}
		if (position_m>N)
			position_m=1;
		if (position_m<1)
			position_m=N;

		if (Q==false) {
			system("cls");
			if (position_m!=6)
				cout << " " << item[position_m-1].r << "\n";

			if (position_m==3||position_m==4||position_m==5) {
				for (int i=0; i<U-1; i++) 
					if (position_pm==i+1)
						cout << "* " << i+1 << "." << item[position_m-1].B[i] << " *\n";
					else 
						cout << "  " << i+1 << "." << item[position_m-1].B[i] << " \n";
				if (position_pm==3)
					cout << "* " << 0 << "." << item[position_m-1].B[2] << " *\n";
				else 
					cout << "  " << 0 << "." << item[position_m-1].B[2] << " \n";
			}

			if (position_m==1||position_m==2) {
				for (int i=0; i<M-1; i++) 
					if (position_pm==i+1)
						cout << "* " << i+1 << "." << item[position_m-1].B[i] << " *\n";
					else 
						cout << "  " << i+1 << "." << item[position_m-1].B[i] << " \n";
				if (position_pm==4)
					cout << "* " << 0 << "." << item[position_m-1].B[3] << " *\n";
				else 
					cout << "  " << 0 << "." << item[position_m-1].B[3] << " \n";
			}

			position_pm=1;

			do	{
				if (position_m==2) {
					z=getch();
					if (z==224)
						z=getch();
					switch (z) {
					case 49:
						position_pm=1;
						break;
					case 50:
						position_pm=2;
						break;
					case 51:
						position_pm=3;
						break;
					case 52:
						position_pm=4;
						break;
					case 48:
						position_pm=4;
						break;
					case 80:
						position_pm++;
						break;
					case 72:
						position_pm--;
						break;
					case 27:
						Q=true;
						position_pm=1;
						break;
					default:
						break;
					}

					if (z==13&&position_pm==1) {
						system("cls");
						p1.DelBegin();
						system("cls");
					}

					if (z==13&&position_pm==2) {
						system("cls");
						p1.DelBack();
						system("cls");
					}

					if (z==13&&position_pm==3) {
						system("cls");
						p1.DelAll();
						system("cls");
					}

					if (position_pm>M)
						position_pm=4;
					if (position_pm<1)
						position_pm=1;

					system ("cls");
					cout << " " << item[position_m-1].r << "\n";

					for (int i=0; i<M-1; i++)	
						if (position_pm==i+1) 
							cout << "* " << i+1 << "." << item[position_m-1].B[i] << " *\n";
						else 
							cout << "  " << i+1 << "." << item[position_m-1].B[i] << " \n";
					if (position_pm==4)
						cout << "* " << 0 << "." << item[position_m-1].B[3] << " *\n";
					else 
						cout << "  " << 0 << "." << item[position_m-1].B[3] << " \n";

					if (position_pm==4) 
						switch (z) {
						case 13:
							Q=true;
							position_pm=1;
							break;
					}
				}

				if (position_m==1) {
					z=getch();
					if (z==224)
						z=getch();
					switch (z) {
					case 49:
						position_pm=1;
						break;
					case 50:
						position_pm=2;
						break;
					case 51:
						position_pm=3;
						break;
					case 52:
						position_pm=4;
						break;
					case 48:
						position_pm=4;
						break;
					case 80:
						position_pm++;
						break;
					case 72:
						position_pm--;
						break;
					case 27:
						Q=true;
						position_pm=1;
						break;
					default:
						break;
					}

					if (z==13&&position_pm==1) {
						system("cls");

						do
						{
							cout << "Введите ключ элемента: ";
							error = 0;
							cin >> tmp.key;
							if( cin.fail() ) // если ошибка при вводе
							{
								cout << "Количество указано неверно, должно быть число\n";
								error = 1;
							}
							cin.clear(); fflush(stdin); // очистка буфера ввода
						}
						while(error == 1);
						
						cout << "Введите название элемента: ";
						cin.sync();
						getline(cin, tmp.name);
						cin.clear(); fflush(stdin); // очистка буфера ввода
				
						p1.AddFront(tmp.name,tmp.key); // добавление элемента в начало списка
						system("cls"); // очистка экрана
					}

					if (z==13&&position_pm==2) {
						system("cls");
						do
						{
							cout << "Введите ключ элемента: ";
							error = 0;
							cin >> tmp.key;
							if( cin.fail() ) // если ошибка при вводе
							{
								cout << "Количество указано неверно, должно быть число\n";
								error = 1;
							}
							cin.clear(); fflush(stdin); // очистка буфера ввода
						}
						while(error == 1);
						
						cout << "Введите название элемента: ";
						cin.sync();
						getline(cin, tmp.name);
						cin.clear(); fflush(stdin); // очистка буфера ввода
				
						p1.AddBack(tmp.name,tmp.key); // добавление элемента в конец списка
						system("cls"); // очистка экрана
					}

					if (z==13&&position_pm==3) {
						system("cls");
						int count;
						int error;

						do
						{
							cout << "Введите число элементов: ";
							error = 0;
							cin >> count;
							if( cin.fail() ) // если ошибка при вводе
							{
								cout << "Ключ указан неверно, должно быть число\n";
								error = 1;
							}
							cin.clear(); fflush(stdin); // очистка буфера ввода
						}
						while(error == 1);						
						
						p1.AddAuto(count); // добавление элемента в конец списка
						system("cls"); // очистка экрана
					}

					if (position_pm>M)
						position_pm=4;
					if (position_pm<1)
						position_pm=1;

					system ("cls");
					cout << " " << item[position_m-1].r << "\n";

					for (int i=0; i<M-1; i++)	
						if (position_pm==i+1) 
							cout << "* " << i+1 << "." << item[position_m-1].B[i] << " *\n";
						else 
							cout << "  " << i+1 << "." << item[position_m-1].B[i] << " \n";
					if (position_pm==4)
						cout << "* " << 0 << "." << item[position_m-1].B[3] << " *\n";
					else 
						cout << "  " << 0 << "." << item[position_m-1].B[3] << " \n";

					if (position_pm==4) 
						switch (z) {
						case 13:
							Q=true;
							position_pm=1;
							break;
					}
				}

				if (position_m==4) {
					v=getch();
					if (v==224)
						v=getch();
					switch (v) {
					case 48:
						position_pm=3;
						break;
					case 49:
						position_pm=1;
						break;
					case 50:
						position_pm=2;
						break;
					case 51:
						position_pm=3;
						break;
					case 80:
						position_pm++;
						break;
					case 72:
						position_pm--;
						break;
					case 27:
						Q=true;
						position_pm=1;
						break;
					default:
						break;
					}

					if (v==13&&position_pm==1) {
						system("cls");
						if (first) {
							p1.Print();
							cout << "Нажмите \"R\" для возврата:\n";
							char t;
							do {
								cin >> t;
							}
							while (t!='R'&&t!='r');

							switch (t)
							{ case 'R':
								system("cls");
								Q=true;
								break;
							}
						}
						else 
							cout << "В списке 0 элементов. Просмотр недоступен";
						system("cls");	
					}

					if (v==13&&position_pm==2) {
						system("cls");
						if (first) 
							p1.Print_list();
						system("cls");
					}

					if (position_pm>U)
						position_pm=3;
					if (position_pm<1)
						position_pm=1;

					system ("cls");
					cout << " " << item[position_m-1].r << "\n";

					for (int i=0; i<U-1; i++)	
						if (position_pm==i+1) 
							cout << "* " << i+1 << "." << item[position_m-1].B[i] << " *\n";
						else 
							cout << "  " << i+1 << "." << item[position_m-1].B[i] << " \n";
					if (position_pm==3)
						cout << "* " << 0 << "." << item[position_m-1].B[2] << " *\n";
					else 
						cout << "  " << 0 << "." << item[position_m-1].B[2] << " \n";

					if (position_pm==3) 
						switch (v) {
						case 13:
							Q=true;
							position_pm=1;
							break;
					}
				}

				if (position_m==3) {
					v=getch();
					if (v==224)
						v=getch();
					switch (v) {
					case 48:
						position_pm=3;
						break;
					case 49:
						position_pm=1;
						break;
					case 50:
						position_pm=2;
						break;
					case 51:
						position_pm=3;
						break;
					case 80:
						position_pm++;
						break;
					case 72:
						position_pm--;
						break;
					case 27:
						Q=true;
						position_pm=1;
						break;
					default:
						break;
					}

					if (v==13&&position_pm==1) {
						system("cls");				
						p1.Edit_Average(); // редактирование элемента в середине списка
						system("cls"); // очистка экрана
					}

					if (v==13&&position_pm==2) {
						system("cls");
						p1.Edit_End(); // редактирование элемента в конце списка
						system("cls"); // очистка экрана
					}

					if (position_pm>U)
						position_pm=3;
					if (position_pm<1)
						position_pm=1;

					system ("cls");
					cout << " " << item[position_m-1].r << "\n";

					for (int i=0; i<U-1; i++)	
						if (position_pm==i+1) 
							cout << "* " << i+1 << "." << item[position_m-1].B[i] << " *\n";
						else 
							cout << "  " << i+1 << "." << item[position_m-1].B[i] << " \n";
					if (position_pm==3)
						cout << "* " << 0 << "." << item[position_m-1].B[2] << " *\n";
					else 
						cout << "  " << 0 << "." << item[position_m-1].B[2] << " \n";

					if (position_pm==3) 
						switch (v) {
						case 13:
							Q=true;
							position_pm=1;
							break;
					}
				}

				if (position_m==5) {
					v=getch();
					if (v==224)
						v=getch();
					switch (v) {
					case 48:
						position_pm=3;
						break;
					case 49:
						position_pm=1;
						break;
					case 50:
						position_pm=2;
						break;
					case 51:
						position_pm=3;
						break;
					case 80:
						position_pm++;
						break;
					case 72:
						position_pm--;
						break;
					case 27:
						Q=true;
						position_pm=1;
						break;
					default:
						break;
					}

					if (v==13&&position_pm==1) {
						system("cls");
						p1.Upload();
						system("cls");		
					}

					if (v==13&&position_pm==2) {
						system("cls");
						p1.Unload();
						system("cls");
					}

					if (position_pm>U)
						position_pm=3;
					if (position_pm<1)
						position_pm=1;

					system ("cls");
					cout << " " << item[position_m-1].r << "\n";

					for (int i=0; i<U-1; i++)	
						if (position_pm==i+1) 
							cout << "* " << i+1 << "." << item[position_m-1].B[i] << " *\n";
						else 
							cout << "  " << i+1 << "." << item[position_m-1].B[i] << " \n";
					if (position_pm==3)
						cout << "* " << 0 << "." << item[position_m-1].B[2] << " *\n";
					else 
						cout << "  " << 0 << "." << item[position_m-1].B[2] << " \n";

					if (position_pm==3) 
						switch (v) {
						case 13:
							Q=true;
							position_pm=1;
							break;
					}
				}

				if (position_m==6) {
					cout << "Вы действительно хотите выйти?\n"; 
					for (int i=0; i<2; i++)	{
						if (position_pm==i+1) 
							cout << "* " << item[position_m-1].B[i] << " *\n";
						else 
							cout << "  " << item[position_m-1].B[i] << " \n";
					}

					w=getch();
					if (w==224)
						w=getch();
					switch (w) {
					case 48:
						position_pm=2;
					case 49:
						position_pm=1;
						break;
					case 50:
						position_pm=2;
						break;
					case 80:
						position_pm++;
						break;
					case 72:
						position_pm--;
						break;
					case 27:
						Q=true;
						position_pm=1;
						break;
					}

					if (position_pm>2)
						position_pm=1;
					if (position_pm<1)
						position_pm=2;

					system ("cls");

					if (position_pm==1) 
						switch (w) {
						case 13:
							Q=true;
							position_pm=1;
							break;
						}

					else if (position_pm==2) 
						switch (w) {
						case 13:
							exit(1);
							break;
						}
				}
			}
			while (Q==false);
		}

		if (Q==true) {
			system("cls");
			for (int i=0; i<N-1; i++) 
				if (position_m==i+1)
					cout << "* " << i+1 << "." << item[i].r << " *\n";
				else 
					cout << "  " << i+1 << "." << item[i].r << " \n";
			if (position_m==6)
				cout << "* " << 0 << "." << item[5].r << " *\n";
			else 
				cout << "  " << 0 << "." << item[5].r << " \n";
		}
	}
}

int _tmain(int argc, _TCHAR* argv[])
{	List p1;
	p1.Menu();
	return 0;
}


