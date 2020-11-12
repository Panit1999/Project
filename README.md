#include <iostream>
using namespace std;
int sum = 0;
int Data[100][5];
string Name[10],Sub[10],Phone[10];
int id[10],idCi[10];
int Room[10][4];
int idCia = 1;
void Insert_Accout();
int Insert_Room();
void CheckIn();
void CheckOut();
void Show();
void Dataroom();
int main(){
	int Choice = 0;
	int out = 0,a = 0;
	for(int i = 0;i < 10;i++){
        Room[i][0] = 0;Room[i][1] = 0;Room[i][2] = 0;Room[i][3] = 0;Room[i][4] = 0;
    }
    for(int i = 0;i < 10;i++){
        idCi[i] = 0;
    }
	//Dataroom(Data);
	do{
		cout<<"=======Main======= \n";
		cout<<"1.Insert Accout \n";
		cout<<"2.Insert Room \n";
		cout<<"3.CheckIn \n";
		cout<<"4.CheckOut\n";
		cout<<"5.Show\n";
		cout<<"Enter Choice: \n";
		cin>>Choice;
		if(Choice == 1)Insert_Accout();
		else if(Choice == 2){a = Insert_Room();cout<<a<<endl;}
		else if(Choice == 3)CheckIn();
		else if(Choice == 4)CheckOut();
		else if(Choice == 5)Show();
		else out = 1;
	}while(out != 1);
	return 0;
}
int Insert_Room(){
            int R,Air,AirP,RP;
            cout<<"Enter Room + Air [Number]: ";
            cin>>Air;
            cout<<"Enter Room + Air [Price]: ";
            cin>>AirP;
            cout<<"Enter Room Normal [Number]: ";
            cin>>R;
            cout<<"Enter Room Normal [Price]: ";
            cin>>RP;
            sum = R+Air;
            for(int i = 0;i < sum;i++){
                if(i < Air){
                        Data[i][0] = 100 + i;
        				Data[i][1] = 1;//type
        				Data[i][2] = 1;//status
        				Data[i][3] = AirP;//Price
        				Data[i][4] = 0;//idCia
                }else{
                        Data[i][0] = 100 + i;
        				Data[i][1] = 2;
        				Data[i][2] = 1;
        				Data[i][3] = RP;
        				Data[i][4] = 0;
                }
            }
            for(int i = 0;i< sum;i++){
        	        cout << Data[i][0] << " " << Data[i][1]<< " " << Data[i][2] << " " 
        	        << Data[i][3]<< " " << Data[i][4]<<"\n";
        	}
        return(sum);
}
void Insert_Accout(){
    string NameN,SubN,PhoneN;
    int ida;
    cout<<"Enter Guest Name : ";
    cin>>NameN;
    cout<<"Enter Guest Surename : ";
    cin>>SubN;
    cout<<"Enter Guest Phone : ";
    cin>>PhoneN;
    cout<<"Enter Guest ID : ";
    cin>>ida;
    for(int i = 0;i < 10;i++){
        if(idCi[i] == 0){
            idCi[i] = idCia;
            Name[i] = NameN;
            Sub[i] = SubN;
            Phone[i] = PhoneN;
            id[i] = ida;
            idCia = idCia + 1;
            break;
        }
    }
    for(int i = 0;i < 10;i++){cout<< idCi[i]<< " " << Name[i] << " " << Sub[i] <<" "<<Phone[i]<<" " <<id[i]<<"\n";}
}
void CheckIn(){
    string type = " ",status = " ",Exname = " ";
    for(int i = 0;i< sum;i++){
        for(int j = 0;j< 10;j++){
            if(Data[i][4] == idCi[j])Exname = Name[j];
        }
        if(Data[i][1] == 1){type = "Room+Air";}else type = "Room Normal";
        if(Data[i][2] == 1){status = "Empty";}else status = "not Empty";
        cout << Data[i][0] << " " << type << " " << status << " " 
    << Data[i][3]<< " " << Exname <<"\n";
    }
    string Deposit,RoomP,EnW;
    int RoomID,Guest;
    cout<<"Guest ID : ";
    cin>>Guest;
    cout<<"Room ID : ";
    cin>>RoomID;
    cout<<"Pay Deposit (Y/N) (มัดจำ):";
    cin>>Deposit;
    cout<<"Pay Room (Y/N) (ค่าห้อง):";
    cin>>RoomP;
    cout<<"Pay Electricity|Water bill (Y/N) (ไฟ | น้ำ):";
    cin>>EnW;
    for(int i = 0;i < sum;i++){
        if(RoomID == Data[i][0]){
            if(Data[i][2] != 1 && Data[i][4] != Guest)cout<<"Room is not Empty \n";
            else if(Data[i][2] != 1 && Data[i][4] == Guest){
                for(int i = 0;i < 10;i++){
                    if(Room[i][0] == RoomID){
                        if(Deposit == "Y" || Deposit == "y")Room[i][1] = 1;else Room[i][1] = 2;
                        if(RoomP == "Y" || RoomP == "y")Room[i][2] = 1;else Room[i][2] = 2;
                        if(EnW == "Y" || EnW == "y")Room[i][3] = 1;else Room[i][3] = 2;
                        cout<<"---Successfull--- \n";
                        break;
                    }}}
            else {
                Data[i][2] = 2;
                Data[i][4] = Guest;
                for(int i = 0;i < 10;i++){
                    if(Room[i][0] == 0){
                        if(Deposit == "Y" || Deposit == "y")Room[i][1] = 1;else Room[i][1] = 2;
                        if(RoomP == "Y" || RoomP == "y")Room[i][2] = 1;else Room[i][2] = 2;
                        if(EnW == "Y" || EnW == "y")Room[i][3] = 1;else Room[i][3] = 2;
                        Room[i][0] = RoomID;
                        cout<<"---Successfull--- \n";
                        break;
                    }}
                for(int i = 0;i < 10;i++){
                    cout<<Room[i][0]<<" "<<Room[i][1]<<" "<<Room[i][2]<<" "<<Room[i][3]<<" \n";
                }}}}}
void CheckOut(){
    string Deposit,RoomP,EnW;
    int RoomID,Guest,D,R,E;
    cout<<"Room ID : ";
    cin>>RoomID;
    for(int i = 0;i < 10;i++){
        if(Room[i][0] == RoomID){
            if(Room[i][1] == 1 && Room[i][2] == 1 && Room[i][3] == 1){
                Room[i][0] = 0;
                Room[i][1] = 0;
                Room[i][2] = 0;
                Room[i][3] = 0;
                for(int j = 0;j< sum;j++){
                    if(RoomID == Data[j][0]){
                        Data[j][2] = 1;
                        for(int x = 0;x< 10;x++){
                            if(Data[j][4] == idCi[x]){
                                idCi[x] = 0;
                                Name[x] = " ";
                                Sub[x] = " ";
                                Phone[x] = " ";
                                id[x] = 0;
                                Data[j][4] = 0;
                                cout<<"***Checkout Successfull***\n";
                                break;
                            }}}}}
            else {
                cout<<"!!!not paid yet!!! \n";
                cout<<"!Comeback to Pay! \n";
            }}}
    for(int i = 0;i < 10;i++){
                    cout<<Room[i][0]<<" "<<Room[i][1]<<" "<<Room[i][2]<<" "<<Room[i][3]<<" \n";
    }}

void Show(){
    string type = " ",status = " ",Exname = " ",Deposit = " ",RoomP = " ",EnW = " ",Suba,Phonea;
    int ida,idCia;
    for(int i = 0;i< sum;i++){
        for(int j = 0;j< 10;j++){
            if(Data[i][4] == idCi[j]){
                idCia = idCi[j];
                Exname = Name[j];
                Suba = Sub[j];
                Phonea = Phone[j];
                ida = id[j];
            }
        }
        for(int a = 0;a < 10;a++){
            if(Data[i][0] == Room[a][0]){
                if(Room[a][1] == 1)Deposit = "paid";else Deposit = "not pay yet";
                if(Room[a][2] == 1)RoomP = "paid";else RoomP = "not pay yet";
                if(Room[a][3] == 1)EnW = "paid";else EnW = "not pay yet";
            }
        }
        if(Data[i][1] == 1){type = "Room+Air";}else type = "Room Normal";
        if(Data[i][2] == 1){status = "Empty";}else status = "not Empty";
        cout << Data[i][0] << " " << type << " " << status << " " << Data[i][3]<<" "<< idCia <<
        " " << Exname <<" "<<Suba<<" "<<Phonea<<" "<<ida<<" "<<Deposit<<" "<<RoomP<<" "<<EnW <<"\n";
        type = " ",status = " ",Exname = " ",Deposit = " ",RoomP = " ",EnW = " ",Suba = " ",Phonea = " ";
    }}
    
    
