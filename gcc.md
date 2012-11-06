[content]: https://github.com/1184893257/simplelinux/blob/master/README.md#content

[��Ŀ¼][content]

<a name="top"></a>

<h1 align="center">�������ͻ��۽�
</h1>

��������� linux �±�д C ����
��ô�㽫�������Ϭ���ķ�����

---

## ������

����һ��C����max.c����

	#define MAX(a,b) ((a)>=(b)?(a):(b))
	
	int main(){
		int c=MAX(1,2); // עעעע��
		return 0;
	}

`����`����ܼ򵥣����Ƕ����ʹ��һ��MAX�꣬
������ʽ����ǰ�ǻᱻ�滻Ϊ������Ŀ�ģ�
�������ڿ����Ĳ��������������������������������գ�

	gcc -E -o max2.c max.c

`����`*����� -o max2.c ���� gcc 
��Ҫ������������ max2.c �ļ��С�*

�������֣�������ΰɣ�

	# 1 "max.c"
	# 1 "<built-in>"
	# 1 "<������>"
	# 1 "max.c"
	
	
	int main(){
	 int c=((1)>=(2)?(1):(2));
	 return 0;
	}

`����`�������max2.c�е����ݣ�MAX(1,2) ���滻���� 
((1)>=(2)?(1):(2))����ֻ�������������ˣ�

���������������þ����滻�꣬���Ǻ�����Ҷ���̫�á�
�������� �ִ� linux �ں�Դ�����м�ֱ�����õ��˼��£�
��������˵ linux �ں����� C���ꡢ��� д�����ġ�
���ǿ���Ƕ�׵ģ�Ҳ����˵��� ���� �� �Ҳ� 
�л����Գ����ܹ����滻�ĺ꣬
����������൱�����ˡ���ʮ���ַ��ļ򵥵�һ����䣬
������ԭΪ������Ŀʱ�����ܾͱ���߰�ʮ���ַ��ˣ�
Ҫ������������䣬�������ʹ��������ˡ�

�������ں꣬����������һƪ�����ܡ�

---

## ���۽�

����������Ӧ���ǲ�����۽𾦵ģ�
���۽𾦿��Կ�������΢С��ϸ�ڡ�������д�˸�Hello World
��hello.c����

	#include <stdio.h>

	int main(){
		printf("Hello, World!\n");
		return 0;
	}

`����`Hello World �Ͳ��ý����˰ɣ�������������O(��_��)O~��
Ȼ�������û��۽�����һ�£�

	gcc -S -o hello.s hello.c

`����`Hello World �Ļ���ͳ�����(hello.s)��

		.file	"hello.c"
		.section	.rodata
	.LC0:
		.string	"Hello, World!"
		.text
	.globl main
		.type	main, @function
	main:
		pushl	%ebp
		movl	%esp, %ebp
		andl	$-16, %esp
		subl	$16, %esp
		movl	$.LC0, (%esp)
		call	puts
		movl	$0, %eax
		leave
		ret
		.size	main, .-main
		.ident	"GCC: (GNU) 4.5.1 20100924 (Red Hat 4.5.1-4)"
		.section	.note.GNU-stack,"",@progbits

`����`���������Ǻ���������������
����ֻҪ֪����ô�á����۽𾦡������ˣ�
�������ļ�ƪ���ÿ�����ˡ�

---

�����������ͻ��۽���ʵ���ǿ��ضϱ������
�õ��м����ģ�gcc��������������ǣ�

	Ԥ����->����->���->����

`����`ʹ�ò�ͬ�ı���ѡ����Եó���ͬ���м���

<table border="1">
 <tr>
  <th>����׶�</th>
  <th>����</th>
  <th>�ضϺ�Ĳ���</th>
 </tr>
 <tr>
  <td></td>
  <td></td>
  <td>CԴ����</td>
 </tr>
 <tr>
  <td>Ԥ����</td>
  <td>gcc -E</td>
  <td>�滻�˺��CԴ����(û����#define,#include��),
	ɾ����ע��</td>
 </tr>
 <tr>
  <td>����</td>
  <td>gcc -S</td>
  <td>���Դ����</td>
 </tr>
 <tr>
  <td>���</td>
  <td>gcc -c</td>
  <td>Ŀ���ļ����������ļ���
  �����в��ڴ��ļ��е��ⲿ����������</td>
 </tr>
 <tr>
  <td>����</td>
  <td>gcc</td>
  <td>��ִ�г���һ���ɶ��Ŀ���ļ�������Ӷ��ɣ�
	�������ļ������б����������������ҵõ�</td>
 </tr>
</table>

����Ҳ����ͬѧ������ -c �һ�û���أ�
�������ļ��ķ�������Ҳ���õ������Ǻ��٣��õ���ʱ����˵�ɡ�

[��Ŀ¼][content]