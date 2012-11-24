[content]: https://github.com/1184893257/simplelinux/blob/master/README.md#content

[��Ŀ¼][content]

<a name="top"></a>

<h1 align="center">��������
</h1>

## ǰ��

��������������д�� ���顢�ṹ�塢ָ�� ��֮����д�������õģ�
��Ϊ�������û�ǣ������Щ������
�����Ҿ����������Ļ��ܻ�¶��������δ�������ţ�
���Ի����ȼ򵥵ط���һ�º������ðɣ�
֮���ٲ��ϵ����ƺ������������һ

## CԴ����double.c��

	#include <stdio.h>
	
	int Double(int b)
	{
		int c;
		
		c = b + b;
		++b;	// ��Ӱ�쵽 a ��
		
		return c;
	}
	
	int main()
	{
		int a = 1;
		int d = Double(a);
	
	    printf("a:%d d:%d\n", a, d);
	    return 0;
	}

## �����

	gcc -S double.c

`����`gcc -S double.c Ĭ�Ͼ��ǰѻ��Դ��������� double.s �У�
֮ǰһֱ�� -o ѡ����Ϊ�˱������Ľ���O(��_��)O~��
double.s �е����ݼ򻯺�

<pre><code>Double:<b>
	pushl	%ebp
	movl	%esp, %ebp
	subl	$16, %esp
	movl	8(%ebp), %eax
	addl	%eax, %eax
	movl	%eax, -4(%ebp)
	addl	$1, 8(%ebp)
	movl	-4(%ebp), %eax
	leave
	ret</b>

main:
	pushl	%ebp
	movl	%esp, %ebp
	andl	$-16, %esp
	subl	$32, %esp<b>
	movl	$1, 28(%esp)
	movl	28(%esp), %eax
	movl	%eax, (%esp)
	call	Double</b>
	movl	%eax, 24(%esp)
	movl	$.LC0, %eax
	movl	24(%esp), %edx
	movl	%edx, 8(%esp)
	movl	28(%esp), %edx
	movl	%edx, 4(%esp)
	movl	%eax, (%esp)
	call	printf
	movl	$0, %eax
	leave
	ret
</code></pre>

## ����

����<b>����</b>�����Ƕ� Double ������һ���������á�

�������ڴ� main �����е� 1 ��<b>����</b>ָ�ʼ������

<table border="1">

<tr><td><pre><code>
	movl	$1, 28(%esp)	# a=1
</code></pre></td>
<td rowspan="2"><img src="http://fmn.rrimg.com/fmn056/20121109/1855/original_1Ykq_291900004dfe1191.jpg" />
</td></tr>
<tr><td>
���Ǹ� �ֲ����� a ��ֵ<br>
����ջָ��Ĵ��� esp ���ڵ�ֵ�� 8000��
����ָ��ִ�����ջ���������ͼ
</td></tr>

<tr><td><pre><code>
	movl	28(%esp), %eax
	movl	%eax, (%esp)	# (%esp) = a
</code></pre></td>
<td rowspan="2"><img src="http://fmn.rrimg.com/fmn063/20121109/1855/original_6CEt_3c0400004d8a125d.jpg" />
</td></tr>
<tr><td>
������ָ� a ��ֵ 1 д���˵�ַΪ 8000 ���ڴ�飨4�ֽڣ���
������� b �ɣ�<br>���ڻ���Ҫ���½��ۡ�
</td></tr>

<tr><td><pre><code>
	call	Double
</code></pre></td>
<td rowspan="2"><img src="http://fmn.rrfmn.com/fmn058/20121109/1855/original_cK4p_448e000041101190.jpg" />
</td></tr>
<tr><td>
call ָ���ִ�У��ɷ�Ϊ�������裺<br>
<ol>
	<li>�� call ָ�����һ��ָ��ĵ�ַѹջ
	<li>�� eip �޸�Ϊ Double �ĵ�ַ
</ol>
Ȼ�����ת�� Double ��ȡָ��ִ���ˡ�<br>
���� call ָ��֮������� movl	%eax, 24(%esp) 
�ĵ�ַ�� 1000����ô call ִ�к�
ջ��������Ϊ��ͼ������
</td></tr>

<tr><td><pre><code>
	pushl	%ebp
	movl	%esp, %ebp
</code></pre></td>
<td rowspan="2"><img src="http://fmn.rrfmn.com/fmn058/20121109/1855/original_5Rl9_5de000004db9118f.jpg" />
</td></tr>
<tr><td>
�Ƚ��ɵ� ebp ѹջ��Ȼ������ʱ��� esp ��ֵ�� ebp��
����ῴ����������Ŀ��
</td></tr>

<tr><td><pre><code>
	subl	$16, %esp	# esp -= 16
</code></pre></td>
<td rowspan="2"><img src="http://fmn.rrimg.com/fmn056/20121109/1855/original_7ikk_0fad00004dc5118e.jpg" />
</td></tr>
<tr><td>
Double �ľֲ������ռ����ô�������ˣ���Ȼ�е��˷ѣ�
</td></tr>

<tr><td><pre><code>
	movl	8(%ebp), %eax
	addl	%eax, %eax
	movl	%eax, -4(%ebp)	# c = b + b
	addl	$1, 8(%ebp)		# ++b
</code></pre></td>
<td rowspan="2"><img src="http://fmn.rrimg.com/fmn065/20121109/1855/original_VXpq_05be00004de5118d.jpg" />
</td></tr>
<tr><td>
8(%ebp) ��ǰ�պñ�ʾ 8000 �ڴ�飬
���� 4 ��ָ��� 8000 �ڴ���ֵ���еĴ�����
���ǿ���ȷ�� 8000 ���ǲ��� b��
�� -4(%ebp) ���� c��
</td></tr>

<tr><td><pre><code>
	movl	-4(%ebp), %eax	# eax = c
	leave
	ret
</code></pre></td>
<td rowspan="2"><img src="http://fmn.rrimg.com/fmn056/20121109/1850/original_zq1t_433a00004e92125b.jpg" />
</td></tr>
<tr><td>
�����������β�����ˣ�<b>�����ķ���ֵҪ�洢���ۼӼĴ��� eax ��</b>��
leave ��ͬ����������ָ�<br>
movl %ebp, %esp<br>
popl %ebp<br>
��ս��� Double ʱ������ָ����β��Ӧ��<br>
<b>������Ǿֲ��ռ䱻�����ˣ�ebp Ҳ��ԭ�ˡ�</b>
<p>�� ret ���൱�� popl %eip��
����ͼ���ִ�� call ָ��֮���ָ���ˡ�</p>
��Ȼ Double �����ľֲ��ռ䱻�����ˣ�
�������е�ֵ���Ǳ��ֲ���ģ�һֱ��֮����� printf ������ʱ��
Double �����ľֲ������Լ����������ݲű����ǡ�
</td></tr>

</table>

## ����

����һ�����ķ����������ٴӴ������ϻع�һ�� Double ������

<pre><code>Double:
	pushl	%ebp				#----------ָ֡�� ebp �л�
	movl	%esp, %ebp			#---------/
	subl	$16, %esp			#----------���ؾֲ������ռ�
	movl	8(%ebp), %eax		#\
	addl	%eax, %eax			#-\
	movl	%eax, -4(%ebp)		#-C �Ĳ���
	addl	$1, 8(%ebp)			#/
	movl	-4(%ebp), %eax		#-----������ֵ���浽 eax �Ĵ���
	leave						#--------\
	ret							#---------��ջ���ָ�ָ֡�롢����
</code></pre>

����������������Ϊ����ָ��Ҳ�������������л��֡�

����<b>���� Double ����̫���򵥣�����û�г��ֱ����Ĵ�����ָ��
��eax �Ĵ�������Ҫ������ÿ��������֪�����������淵��ֵ�ģ�
�ں�������󲿷ֿ϶��ᱻ�޸ģ������ӵĺ������ں�������ǰ��
pushl �����޸ĵļĴ��������� ret ֮ǰ popl �Ĵ����Իָ�ԭ����ֵ��</b>

## С��

����ͨ���� Double �����ķ�����
����ע�⵽ ebp �� esp ���������ƣ�
�����о���Ҳͨ�� ebp + ƫ�� �ķ�ʽ������ ���� �� �ֲ�������
���ڿ������ҳ�ŵ�ˣ�<b>esp �� ebp ��ƫ�ƾ���
�ֲ��������ı�����ʽ</b>��
���� ָ֡��Ĵ��� ebp ������ٳ�һƪ�����з�����

����ͬʱ����Ҳ�������Եؿ���ֵ���ݵĹ��̣�
����ǰ�� a ���Ƶ� b��ֵ���������Ƿֱ��ǲ�ͬ���ڴ�飩��
����������� b ֱ�ӱ������ˣ�Ҳ�����ٿ����� a��
������Ȼ���� Double �� ++b �ˣ��� a ��ֵ��ȻΪ 1��
��������н�����£�

	[lqy@localhost temp]$ gcc -o double double.c
	[lqy@localhost temp]$ ./double
	a:1 d:2
	[lqy@localhost temp]$ 

`����`��һƪ���ټ�������ֵ���ݡ�

[��Ŀ¼][content]