jaman - javadoc����������ץ�
============================

����ϲ�����
-----------

Java �� API ��ե���� (javadoc) �򡢥��饹̾�����̾�����
��������ǥ֥饦���Ǥ��륷���륹����ץȤǤ���

�ʲ��Τ褦����ħ������ޤ���

* �ҥ塼�ꥹ�ƥ��å��ޥå��󥰤ǡ��Ǿ�������ʸ�����Ǻ�Ŭ�ʷ��
* ʣ���� javadoc ����ɤ������Ǥ���
* ͽ�ᥤ��ǥå������äƤ���ɬ�פ��ʤ� (��ư���������)

�׵�Ķ�
--------

����Ū�� UNIX ���ޥ�� (grep, sed, gawk(nawk), gzip ��) ��¸�ߤ��� UNIX �Ķ���
Cygwin �Ķ��Ǥ�ư���ޤ���

HTML �ե������֥饦������Ȥ��ˡ�`browse`
�Ȥ���̾���Υץ����� URL ������ˤ��ƸƤӽФ��Τǡ�
ͽ���Ѱդ��Ƥ���ɬ�פ�����ޤ���

���󥹥ȡ�����ˡ
---------------

1. `grep, sed, gawk` �������̤ʾ��ˤ�����ϡ�
   �ե����� `jaman` ����Ƭ�˽񤤤Ƥ��롢�����Υѥ���񤭴����ޤ���
2. �ե����� `jaman` �� `browse` �Ȥ򡢥ѥ����̤ä��ǥ��쥯�ȥ���֤��ޤ���
3. �Ķ��ѿ� `JAMANPATH` �ˡ����������� javadoc
   ���֤��Ƥ���ǥ��쥯�ȥ�� ':' �Ƕ��ڤäƻ��ꤷ�ޤ���
   �����ǻ��ꤹ��ǥ��쥯�ȥ�ϡ�`allclasses-frame.html`
   �����֤��Ƥ���ǥ��쥯�ȥ�Ǥ�����:

   <pre>
export JAMANPATH=/usr/local/jdk1.4/docs/ja/api:$HOME/doc/jdom/apidocs:/usr/local/junit3.7/javadoc:/usr/local/bcel-5.0/docs/api
</pre>

   ���֤Ͻ��פǤ�����ˤ����ΤΤۤ���������ͥ�褵��ޤ���
4. ����ǽ����ϴ�λ�Ǥ���
   �ǽ�θ����¹Ի��ˤϡ�����ǥå����ե�������������Τ�
   �������֤�������ޤ���
   ����ǥå����ե�����ϥۡ���ǥ��쥯�ȥ�β���
   `.jaman.cache/` �ʲ��˺���ޤ���

�Ȥ���
------

### ����Ū�ʻȤ���

`jaman2` �ϥ��ޥ�ɥ饤�󤫤鵯ư���ޤ���

���饹̾�����̾�ΰ�����ɽ��ʸ������Ϥ��ȡ�
����ʸ����˥ޥå����륯�饹/���Ф� javadoc �ե������֥饦����ɽ�����ޤ���
��:

<pre>
$ jaman String        => java.lang.String
$ jaman mkdirs        => java.io.File#mkdirs()
$ jaman awt.List      => java.awt.List
$ jaman List.size     => java.util.List#size()
$ jaman List#size     => java.util.List#size()
$ jaman lang.Object   => java.lang.Object
$ jaman g.Object      => java.lang.Object
</pre>

jaman �θ����ϡ��Ǿ������ϤǺ��ɤη�̤����뤳�Ȥ��ܻؤ��Ƥ��ꡢ
Ϳ����줿�ѥ�����򸵤ˡ��ʤ�٤�Ŭ�ڤʥ���ȥ��ɽ�����褦�Ȥ��ޤ���
�㤨�С�"`io.InputStream`" �򸡺�������硢

* `java.io.InputStream`
* `java.io.InputStreamReader`

��2�Ĥ��ޥå����ޤ�����`java.io.InputStream` �Τۤ���
���Ŭ�� [1] �ʤΤǡ��������ɽ�����ޤ���
�����ơ�¾�� `java.io.InputStreamReader` �Ȥ������䤬����ݤ�
ɸ����Ϥ˽��Ϥ��ޤ���[2]

Ŭ�ڤȻפ��륨��ȥ꤬ʣ�����Ĥ��ä����ˤϡ�
����Υꥹ�Ȥ����դ��ǥ֥饦����ɽ�����ޤ���
�㤨�С�"`List`" �򸡺�����ȡ�

* `java.awt.List`
* `java.util.List`

��2�Ĥ������֤褦�� HTML �ե�������������ơ��֥饦�����̤�ɽ�����ޤ���
�ʤ����������¿������Ȥ� (�ǥե���ȤǤ� 20 ��Ķ�����Ȥ�) �ˤϡ�
����Τߤ�ɽ�����졢����ꥹ�ȤΥ֥饦���ϹԤ��ޤ���

�ޥå����ƥ֥饦�����Ԥʤ�줿�ꡢ����Υꥹ�Ȥ�ɽ�����줿���Ǥ⡢
¾�˲�ǽ���Τ�����䤬����С����λݤ�ɸ����Ϥ˽��Ϥ���ޤ���
�������¿������Ȥ� (�ǥե���ȤǤ� 20 ��Ķ�����Ȥ�) �ˤϡ�
����Τ�ɽ�����ޤ���

### ����¾

* �������饹�ˤ��б����Ƥ��ޤ���

  <pre>
$ jaman Arc2D.D       => java.awt.geom.Arc2D.Double
$ jaman Entry         => java.util.Map.Entry
</pre>

* ʣ���Υѥ��������ꤹ�뤳�Ȥ��Ǥ��ޤ� (AND ����)��
  ʣ���Υѥ��������ꤹ��ȡ������¤ӽ�˽��äơ�
  ���ƤΥѥ�����˥ޥå����륨��ȥ꤬��������ޤ���

  <pre>
$ jaman util setValue    => java.util.Map.Entry#setValue()
$ jaman Out Writer       => java.io.OutputStreamWriter
</pre>

* �����κݤ��羮ʸ���ζ��̤ˤĤ���
  jaman �ϡ��羮ʸ���ζ��̤ˤĤ��ơ�
  �ǥե���ȤǤ� Emacs �饤������ˡ��Ȥ��ޤ���
  �Ĥޤꡢ�ѥ�������꤬���ƾ�ʸ���ʤ顢
  �羮ʸ����̵�뤷�Ƹ������ޤ���
  �ѥ��������ˤҤȤĤǤ���ʸ���������äƤ����顢
  �羮ʸ������̤���������Ԥʤ��ޤ���

  <pre>
$ jaman method     => java.lang.reflect.Method,
                      java.net.HttpURLConnection#method,
                      javax.swing.text.html.HTML.Attribute#METHOD
$ jaman Method     => java.lang.reflect.Method
</pre>

���ޥ�ɥ饤�󥪥ץ����
-----------------------

`usage: jaman [option...] <pattern>...`

���ץ����:

<table>
 <tr><td><code>-path <var>&lt;path&gt;</var></code></td><td>API��ե���󥹤θ����ѥ�����ꤹ�롣�ѥ��� ':' �Ƕ��ڤ��롣</td></tr>
 <tr><td><code>-i</code></td><td>�羮ʸ����̵�뤷��������Ԥʤ���</td></tr>
 <tr><td><code>-c</code></td><td>�羮ʸ������̤���������Ԥʤ���</td></tr>
 <tr><td><code>-s</code>&nbsp;<var>&lt;n&gt;</var>, <code>-show-candidates-max</code>&nbsp;<var>&lt;n&gt;</var>&nbsp;&nbsp;</td><td>n ��ʲ��θ��䤬���ä���硢��ά����������ɽ�����롣'all' ����ꤷ�����ˤϾ�¤��ߤ��ʤ���n �Υǥե���Ȥ� 20��</td></tr>
</table>

�饤����
----------

jaman �� MIT �饤���󥹤β������ۤ���ޤ���
�ܤ����� `jaman` ������ץȥե��������Ƭ�ˤ��뵭�Ҥ򻲾Ȥ��Ƥ���������

---

<dl>
 <dt>*1:</dt>
 <dd><p>��Ŭ�ڡפ��ɤ�����Ƚ�Ǥϡ��ѥ�����ñ��ñ�̤ǥޥå����뤫��
     substring �Ȥ��ƥޥå����뤫���ˤ�äƤʤ���ޤ���
     ñ��ñ�̤ǥޥå������ΤΤۤ���������Ŭ�ڡפǤ���Ȥߤʤ��졢
     substring �Ȥ��ƥޥå������Τ��ͥ�褵��ޤ���</p></dd>
 <dt>*2:</dt>
 <dd><p>�դˡ�<code>InputStreamReader</code> ��ɽ�����������ˤϡ�
     <code>jaman InputStreamR</code> ���ȼ¹Ԥ��Ʋ�������</p>
     <p>���̤ˡ��ǰ��ξ��Ǥ⡢¾�ȶ��̤Ǥ����ˡ�����
      ��û��ʸ�������ꤹ��С���Ū�Υ��饹���ϥ��Ф�
      ��ȯ�ǥ֥饦���Ǥ��ޤ���
     </p>
<pre>
% jaman l.List      =&gt; java.util.List
% jaman g.Obj       =&gt; java.lang.Object
% jaman r#substr    =&gt; java.lang.StringBuffer#substring()
</pre>
 </dd>
</dl>

