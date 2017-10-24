#include<stdio.h>
#include<assert.h>

//将两个文件中的字符合并（按字母排序），输出到另一个文件中
void Merge(const char *c,const char *a,const char *b)
{
	FILE *fa = fopen(a,"r");
	FILE *fb = fopen(b,"r");
	FILE *fc = fopen(c,"r");
	assert(fa != NULL && fb != NULL && fc != NULL);

	char arr[100];
	char brr[100];
	char crr[100];

	int len1 = fread(arr,1,100,fa);
	int len2 = fread(brr,1,100,fb);

	int i = 0;
	int j = 0;
	int k = 0;

	while(i < len1 && j < len2)
	{
		if(arr[i] < brr[i])
		{
			crr[k++] = arr[i++];
		}
		else
		{
			crr[k++] = brr[j++];
		}
	}

	while(i < len1)
	{
		crr[k++] = arr[i++];
	}

	while(j < len2)
	{
		crr[k++] = brr[j++];
	}

	fwrite(crr,1,len1 + len2,fc);

	fclose(fa);
	fclose(fb);
	fclose(fc);
}

int main()
{
	char *patha = "H:\\1.1.txt";
	char *pathb = "H:\\1.2.txt";
	char *pathc = "H:\\1.3.txt";

	Merge(patha,pathb,pathc);
	return 0;
}
