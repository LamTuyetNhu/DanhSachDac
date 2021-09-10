#include<stdio.h> 

#define MaxLength 100

typedef int ElementType; //kieu cac pt
typedef int Position; 	 //vi tri cac pt 
typedef struct {
	ElementType Elements[MaxLength];
	Position Last;  
}List;
//Vi tri dau tien 
Position first(List L) {
	return 1;
}
//Vi tri cuoi cung 
Position endList(List L) {
	return L.Last+1;
}
//Vi tri tiep theo 
Position next(Position p, List L) {
	return p + 1;
}
//Vi trí truoc vi tri p
Position Previous(Position p, List L){
	return p - 1;
} 
//Gia tri tai vi tri p
Position Retrieve(Position p, List L){
	return L.Elements[p-1];
}
 //kt do dai ds co bang 0 khong?
int EmtyList(List L){
 	return L.Last == 0; 
 } 
 //Ktra ds co bang MaxLength hay k?
int fullList(List L) {
 	return L.Last == MaxLength;
 } 
//khoi tao ds rong 
void makenullList(List *pL) {
	pL -> Last = 0;
} 
//sap xep theo thu tu tang dan
void sort(List *pL) {
	int p, q;
	for(p = 0; p< pL->Last-1; p++)
		for(q = p + 1; q < pL->Last; q++)
			if(pL->Elements[p] > pL->Elements[q]){
				int temp = pL->Elements[p];
				pL->Elements[p] = pL->Elements[q];
				pL->Elements[q] = temp;
			}
		} 	
//ktr X co trong ds k? neu co return1, nguoc lai return 0
int member(ElementType x, List L){
	Position i;
	for(i=0; i<L.Last; i++)
		if(L.Elements[i] == x)
			return 1;
	return 0;
}
//them pt vao cuoi ds
void insertSet(ElementType x, List *pL) {
	pL->Elements[pL->Last] = x;
	pL->Last++;
}
//nhap tap hop tu ban phim
void readSet(List *pL) {
	makenullList(pL);
	int n;
	scanf("%d", &n);
	ElementType x, i;
	for(i=1; i<=n; i++){
		scanf("%d", &x);
		if(member(x, *pL) == 0)
			insertSet(x, pL); 
	}
}
//ktr pt X  trong ds hay khong
int locate(ElementType x, List L) {
	Position p;
	for(p=1; p<=L.Last; p++) {
		if(L.Elements[p-1] == x)
			return p;//tai vi tri p
	}
	return L.Last + 1; //tai vi tri cuoi cung +1
}
//duyet ds, hien thi so le
void printOddNumbers(List L) {
	Position i; 
	for(i=0; i< L.Last; i++)
		if(L.Elements[i] % 2 != 0)
			printf("%d ", L.Elements[i]); 
} 
//copy so chan vao cuoi ds rong 
void copyEvenNumbers(List L1, List *pL2){
	makenullList(pL2);
	Position i;
	for(i=0; i<L1.Last; i++)
		if(L1.Elements[i] % 2 == 0){
			pL2->Elements[pL2->Last] = L1.Elements[i];
			pL2->Last++; 
		}
} 
//them pt X vao ds o vi tri p
void insertList(ElementType x, Position p, List *pL){
	if(pL->Last == MaxLength)
		printf("Danh sach day\n");
	else if(p<1 || p > pL->Last+1)
			printf("Vi tri khong hop le\n");
		else {
			Position i;
			for(i=pL->Last; i>=p-1; i--)
				pL->Elements[i] = pL->Elements[i-1];
			pL->Last++; ;
			pL->Elements[p-1] = x;
	}
} 
//them x vao cuoi ds
void readList(List *pL) {
    makenullList(pL);
    int n, i;
    ElementType x;
    scanf("%d", &n);
    for(i=1; i<=n; i++){
        scanf("%d", &x);
        pL->Elements[pL->Last] = x;
        pL->Last++;
    }
}
//in ds ra man hinh
void printList(List L){
	Position i;
	for(i=0; i<L.Last; i++)
		printf("%d ", L.Elements[i]);
	printf("\n"); 
} 
//ham tim tap hop hieu cua 2 tap hop
void difference(List L1, List L2, List *pL){
	makenullList(pL);
	int i;
	for(i=0; i<L1.Last; i++){
		if(member(L1.Elements[i], L2) == 0)
			insertSet(L1.Elements[i], pL); 
	} 
} 
//tap hop cua 2 ds
void unionSet(List L1, List L2, List *pL){
	makenullList(pL);
	int i;
	for(i=0; i<L1.Last; i++)
		insertSet(L1.Elements[i], pL);
	for(i=0; i<L2.Last; i++)
		if(member(L2.Elements[i], L1) == 0)
			insertSet(L2.Elements[i], pL);
} 
//xoa pt x tai vi tri p cua ds
void deleteList(Position p, List *pL){
	if(pL->Last == MaxLength)
		printf("Danh sach day\n");
	else if(p<1 || p > pL->Last)
			printf("Vi tri khong hop le\n");
		else {
			Position i;
			for(i=p; i< pL->Last; i++)
				pL->Elements[i-1] = pL->Elements[i];
			pL->Last--;
		}
}
//xoa pt x xuat hien dau tien
void erase(ElementType x, List *pL) {
	Position p = locate(x, *pL);
	if(p!=pL->Last+1)
		deleteList(p, pL);
}
//chuan hoa, luot bo cac gt trung nhau
//goi ham delete
void normalize(List *pL){
	Position p = 1;
	while(p != pL->Last+1){
		Position q = p + 1 ;
		while(q != pL->Last+1){
			if(pL->Elements[p-1] == pL->Elements[q-1]){
				deleteList(q, pL);
				q--; 
			}
			q++; 
		}
		p++;
	}
}
//tap hop giao cua 2 ds
void intersection(List L1, List L2, List *pL){
	makenullList(pL); 
	Position i;
	for(i=0; i<L1.Last; i++)
		if(member(L1.Elements[i], L2) == 1)
			insertSet(L1.Elements[i], pL);
} 
//xoa tat ca cac pt x trong ds
void removeAll(ElementType x, List *pL){
	while(locate(x, *pL) <= pL->Last)
		deleteList(locate(x, *pL), pL); 
} 
//tinh trung binh cong cua cac pt trong ds
float getAvg(List L) {
	int S = 0;
	Position i;
	if(L.Last > 0){
		for(i=0; i<L.Last; i++)
			S += L.Elements[i];
		return S/L.Last ;
	}
	return -10000.0000; 
}
