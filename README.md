# Find-numbers-in-a-set-
#c
첫째 줄에 n, m이 주어진다. m은 입력으로 주어지는 연산의 개수이다. 다음 m개의 줄에는 각각의 연산이 주어진다. 합집합은 0 a b의 형태로 입력이 주어진다. 이는 a가 포함되어 있는 집합과, b가 포함되어 있는 집합을 합친다는 의미이다. 두 원소가 같은 집합에 포함되어 있는지를 확인하는 연산은 1 a b의 형태로 입력이 주어진다. 이는 a와 b가 같은 집합에 포함되어 있는지를 확인하는 연산이다. a와 b는 n 이하의 자연수 또는 0이며 같을 수도 있다. 1로 시작하는 입력에 대해서 한 줄에 하나씩 Yes/No를 출력하는 프로그램을 만들어보자!

#유니온파인드 알고리즘
1.유니온 파인드는 그래프 알고리즘으로 두 노드가 같은 그래프에 속하는지 판별하는 알고리즘입니다.
2.노드를 합치는 Union연산과 노드의 루트 노드를 찾는 Find연산으로 이루어집니다.

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int *parent;
int findparent(int x){ //findparent == Find
	if(parent[x]==x) return x;
	parent[x]=findparent(parent[x]); //값이 서로 다르면 부모값을 넣고 찾기  
	return parent[x];
}


void combine(int a,int b){ //combine == Union  
	int parentx=findparent(a);
	int parenty=findparent(b);
	if(parentx<parenty){ parent[parentx]=parenty; //더 큰수를 작은수 부모값에 넣는다  
		}
	else{parent[parenty]=parentx;}
}


int main(){
	int n,m,i,j,com,a,b;
	scanf("%d %d",&n,&m);
	parent=malloc(sizeof(int)*(n+1));
	for(j=1;j<n+1;j++) parent[j]=j;
	for(i=0;i<m;i++){
		scanf("%d %d %d",&com,&a,&b);
		if(com==0){
			combine(a,b);}
		else if(com==1){
			int parenta=findparent(a);
			int parentb=findparent(b);
			if(parenta==parentb){printf("Yes\n");}
			else{printf("No\n");}}
	}
	return 0;	
}
