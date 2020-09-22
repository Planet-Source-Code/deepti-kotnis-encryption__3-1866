<div align="center">

## Encryption


</div>

### Description

This code implements 3 encryption algorithms one after another i.e. 3 level encryption is achieved.

3 Algorithms used are:

1.Reversing Algorithm

2.Grille's Method

3.Word-Alphabet Correlation Algorithm
 
### More Info
 
Enter any word or phrase without any white spaces containing only lowercase letters for best results.

Gives you back the word/phrase entered in the encrypted format.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Deepti Kotnis](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/deepti-kotnis.md)
**Level**          |Beginner
**User Rating**    |3.3 (10 globes from 3 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+, UNIX C\+\+
**Category**       |[Algorithms](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/algorithms__3-29.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/deepti-kotnis-encryption__3-1866/archive/master.zip)

### API Declarations

```
#include <stdio.h>
#include <string.h>
```


### Source Code

```
#include <stdio.h>
#include <string.h>
void Encryption(char *originalStr);
void Decryption(int *encrypt,int origlen,int encryptlen);
#define kEncryptionKey 3
char GrillArray[2][100],phrase[] = {"the quick brown fox jumps over the lazy dog"};
int grilllen = 0;
int main (void)
{
  char originalStr[100];
  printf("please enter a word or phrase without any white spaces containing only lowercase characters(a-z):");
  scanf("%s",originalStr);
  Encryption(originalStr);
  return 0;
}
void Encryption(char *originalStr)
{
	char rev[100],grill[100];
	int encrypt[100];
	int choice = 0,origlen = strlen(originalStr);
	int i,k,l,m=0,index=0,wordCnt=0,letterCnt=0;
	k = strlen(originalStr)-1;
	for(i=0;i<strlen(originalStr);i++)
	{
		rev[i] = originalStr[k];
		k--;
	}
	rev[i] = '\0';
	k = 0;
	for(i=0;i<strlen(originalStr);i++)
	{
		if(i==index)
		{
			GrillArray[0][k] = i;
			GrillArray[1][k] = rev[i];
			index = index + kEncryptionKey;
			k++;
		}
		else
		{
			grill[m] = rev[i];
			m++;
		}
	}
	grilllen = k;
	grill[m] = '\0';
	k = 0;
	i=0;
	for(l=0;l<strlen(grill);l++)
	{
		k = 0;
		wordCnt = 0;
		letterCnt = 1;
		while(grill[l] != phrase[k])
		{
			if(phrase[k] == ' ')
			{
				wordCnt++;
				letterCnt = 0;
			}
			k++;
			if(phrase[k] != ' ')
				letterCnt++;
		}
		if(grill[l] == phrase[k])
		{
			encrypt[i] = wordCnt+1;
			i++;
			encrypt[i] = letterCnt;
			i++;
		}
	}
	encrypt[i] = '\0';
	printf("\nEncrypted phrase is:");
	for(l=0;l<i;l++)
		printf("%d",encrypt[l]);
	printf("\n\nDo you want to decrypt it? 0:YES 1:NO\n");
	scanf("%d",&choice);
	if(choice == 0)
		Decryption(encrypt,origlen,i);
	else
		printf("Thanx");
}
void Decryption(int *encrypt,int origlen,int encryptlen)
{
	int i,wordCnt=0,k=0,letterCnt,j,m=0,firstindex=0,secondindex;
	char word[6],first[100],second[100],decrypt[100];
	for(i=0;i<encryptlen;i=i+2)
	{
		wordCnt=0,letterCnt=1;
		k=0;
		while(wordCnt != encrypt[i])
		{
			if(phrase[k] == ' ')
			{
				wordCnt++;
				letterCnt = 0;
			}
			letterCnt++;
			k++;
		}
		j=k-2;
		while(phrase[j] != ' ')
		{
			j--;
			if(j == 0)
				break;
		}
		if(j!=0)
			j++;
		m=0;
		while(phrase[j] != ' ')
		{
			word[m] = phrase[j];
			j++;
			m++;
		}
		word[m] = '\0';
		m=0;
		while(m != encrypt[i+1])
			m++;
		first[firstindex] = word[m-1];
		firstindex++;
	}
	first[firstindex] = '\0';
	secondindex = 0;
	i=0;
	j=0;
	while(secondindex < origlen)
	{
		if(secondindex == GrillArray[0][i])
		{
			second[secondindex] = GrillArray[1][i];
			i++;
		}
		else
		{
			second[secondindex] = first[j];
			j++;
		}
		secondindex++;
	}
	second[secondindex] = '\0';
	k = strlen(second)-1;
	for(i=0;i<strlen(second);i++)
	{
		decrypt[i] = second[k];
		k--;
	}
	decrypt[i] = '\0';
	printf("\nDecrypted phrase is:%s",decrypt);
}
```

