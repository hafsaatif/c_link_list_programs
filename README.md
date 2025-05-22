# c++_ link_list_programs
A program consist of link_list and also use vectors.Great program easy code.
#include<iostream>
#include<vector> // Add this
using namespace std;

class item{
	public:
	string data1;
	item* next;
};
class Node{
	public:
	int id;
	item* next;
};
class link_list{
	private:
		Node* head;
		public:
			link_list():head(NULL){}
			void insert_at_beg(int value)
			{
				Node* abc=new Node();
				abc->id=value;
				abc->next=NULL;
				head=abc;
			}
				void insert_at_end(string value)
			{
				item* abc=new item();
				abc->data1=value;
				abc->next=NULL;
				Node* temp1=head;
			if(temp1->next==NULL)
			temp1->next=abc;
			else
			{
				item* temp=temp1->next;
			while(temp->next!=NULL)
			{
				temp=temp->next;
				}
				temp->next=abc;	
			}
		}
			void print()
			{
			Node* temp1=head;
		
			item* temp=temp1->next;
				while(temp!=NULL)
				{
				cout<<temp->data1<<"      ";
				temp=temp->next;
				}
					cout<<temp1->id;
				cout<<endl<<"-----------------"<<endl;
					
			}
			void edit(string input)
			{
				string replace;
			item* temp=head->next;
			if(temp->next->data1==input)
			{
					cout<<"edit expense : ";
				while(temp!=NULL)
				{
				
			cin>>replace;
			temp->data1=replace;
			temp=temp->next;	
				}
				}	
			}
			int delete_expense(string input)
			{
     			int n=0;
			item* temp=head->next;
				while(temp!=NULL)
				{
		        if(temp->data1==input)
		      	{
		     	n=1;
			    return n;	
			     }
				temp=temp->next;	
				}
			}
			bool operator <(link_list c)
			{
				cout<<endl<<endl<<"Expensive item is : "<<endl<<endl;
					cout<<"id     "<<" item   quantity    date        price"<<endl;
			bool n=false;
			item* temp=head->next;
			item* temp1=c.head->next;
			if(head->id>c.head->id)
			{
				while(temp!=NULL)
				{
				cout<<temp->data1<<"      ";
				temp=temp->next;
				}
				cout<<head->id<<endl;
//				cout<<temp->id<<" "<<temp->next->data1<<"  "<<temp->next->next->data1<<endl<<endl;
				n=true;
				}	
				else
				{
			
					while(temp1!=NULL)
				{
				cout<<temp1->data1<<"      ";
				temp1=temp1->next;
				}
				cout<<c.head->id<<endl;
//				cout<<temp->id<<" "<<temp->next->data1<<"  "<<temp->next->next->data1<<endl<<endl;
				n=true;
				}	
				
				//cout<<temp1->id<<" "<<temp1->next->data1<<"  "<<temp1->next->next->data1<<endl<<endl;	

			return n;	
			}
				};
// (Your classes item, Node, and link_list remain unchanged)

int main() {
    cout << "                 -------------------------------" << endl;
    cout << "                 |   EXPENSE TRACKING APP       |" << endl;
    cout << "                 -------------------------------" << endl << endl;

    cout << "id     " << " item   quantity    date        price" << endl;

    int press = 1;
    vector<link_list*> obj; // <<==== Using vector now

    while (press != 5) {
        int choice;
        cout << endl << endl << "****************************************" << endl;
        cout << "* 1- Add expense                       * " << endl;
        cout << "* 2- View all expense                  * " << endl;
        cout << "* 3- Generate a report                 * " << endl;
        cout << "****************************************" << endl << endl;
        cout << "enter choice: ";
        cin >> choice;

        switch (choice) {
        case 1: {
            cout << "1- New expense " << endl << "2- Edit expense " << endl << "3- Delete expense " << endl;
            int expense_choice;
            cout << "enter choice: ";
            cin >> expense_choice;

            if (expense_choice == 1) {
                // Add new expense
                link_list* l = new link_list();

                int data;
                string expense_data;
                cout << "price: ";
                cin >> data;
                l->insert_at_beg(data);
                cout<<"ID : ";
string a;
cin>>a;
                l->insert_at_end(a);
                cout << "item: ";
                cin >> expense_data;
                l->insert_at_end(expense_data);

                cout << "quantity: ";
                cin >> expense_data;
                l->insert_at_end(expense_data);

                cout << "date: ";
                cin >> expense_data;
                l->insert_at_end(expense_data);

                obj.push_back(l);
                l->print();
            } else if (expense_choice == 2) {
                string user;
                cout << "which item you want to edit: ";
                cin >> user;
                for (auto& l : obj) {
                    l->edit(user);
                }
            } else {
                // delete
                string user1;
                cout << "which item you want to delete: ";
                cin >> user1;
                for (int i = 0; i < obj.size(); i++) {
                    if (obj[i]->delete_expense(user1) == 1) {
                        delete obj[i];
                        obj.erase(obj.begin() + i);
                        cout << "Deleted.\n";
                        break;
                    }
                }
            }
            break;
        }
        case 2: {
            for (auto& l : obj) {
                l->print();
            }
            break;
        }
        case 3: {
            if (obj.size() >= 2) {
                for (size_t i = 0; i < obj.size() - 1; ++i) {
                    *obj[i] < *obj[i + 1];
                }
            } else {
                cout << "Not enough expenses to compare.\n";
            }
            break;
        }
        }

        cout << "press 5 to exit: ";
        cin >> press;
    }

    // Cleanup
    for (auto l : obj) {
        delete l;
    }

    return 0;
}

