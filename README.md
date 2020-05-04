<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">

<html><head><meta http-equiv="Content-Type" content="text/html; charset=windows-1252">
<title>Operaciones fundamentales para usuarios de un cluster Rocks</title>
<meta name="description" content="Operaciones fundamentales para usuarios de un cluster Rocks">
<meta name="keywords" content="intensiva">
<meta name="resource-type" content="document">
<meta name="distribution" content="global">

<meta name="Generator" content="LaTeX2HTML v2008">
<meta http-equiv="Content-Style-Type" content="text/css">

<link rel="STYLESHEET" href="./Operaciones fundamentales para usuarios de un cluster Rocks_files/intensiva.css">

<link rel="next" href="">
<link rel="previous" href="">
<link rel="up" href="">
<link rel="next" href="">
</head>

<body>

<div class="navigation">
<a name="tex2html87" href="">
<img align="BOTTOM" border="0" alt="previous" src="./Operaciones fundamentales para usuarios de un cluster Rocks_files/prev.png"></a> 
<a name="tex2html93" href="">
<img align="BOTTOM" border="0" alt="up" src="./Operaciones fundamentales para usuarios de un cluster Rocks_files/up.png"></a> 
<a name="tex2html95" href="">
<img align="BOTTOM" border="0" alt="next" src="./Operaciones fundamentales para usuarios de un cluster Rocks_files/next.png"></a> <div style="background:#9988cc;color:white;">Siguiente: <b><a name="tex2html96" href="http://www.eead.csic.es/compbio/material/programacion_rocks/node4.html">Operaciones fundamentales para administradores de un</a></b>  Sube: <b><a name="tex2html94" href="http://www.eead.csic.es/compbio/material/programacion_rocks/node1.html">Rocks</a></b>  Anterior: <b><a name="tex2html88" href="http://www.eead.csic.es/compbio/material/programacion_rocks/node2.html">Instalaci�n de un cluster Rocks virtual</a></b></div></div>
<!--End of Navigation Panel-->

<h2><a name="SECTION00012000000000000000">
Operaciones fundamentales para usuarios de un cluster Rocks</a>
</h2>

<p>
Si acabas de montar un cluster Rocks o te han dado acceso a uno,
probablemente necesites aprender a usarlo y/o administrarlo. 
Por supuesto tu mejor recurso es la <a name="tex2html15" href="http://www.rocksclusters.org/">documentaci�n oficial Rocks</a>
(que por cierto est� a tu alcance aunque no tengas acceso a Internet, abriendo un navegador en el nodo maestro con la URL 
<code>http://localhost}</code>). 
Si prefieres en espa�ol, te recomiendo el manual 
<a name="tex2html16" href="http://dl.dropbox.com/u/7857160/Shared/RocksPracticalGuide-Zuluaga-Rel1-Jul.08.zip">Linux Clustering con Rocks, una Gu�a Pr�ctica</a>.

</p><p>
Estos son unas cuantas tareas esenciales para aprender a manejar el cluster:

</p><p>

</p><ul>
<li> <i> C�mo encender el cluster  </i> <a name="encendido"></a>
<p>
Si te toca encender el cluster, aseg�rate de que que el nodo maestro est� enchufado a la red el�ctrica y 
oprime el bot�n ON/POWER o equivalente. Puedes ver c�mo discurre el arranque si enchufas una pantalla y un teclado 
al maestro. Si todo va bien, tras los mensajes t�picos de un sistema Linux, llega la linea final de 
<code>login: </code> donde puedes registrarte con tu nombre de usuario.

</p><p>
Ahora puedes encender los nodos secundarios poco a poco o todos a la vez, dependiendo de la potencia de tu
alimentaci�n el�ctrica, d�ndole al bot�n de encendido de cada uno.

</p><p>
Puedes comprobar que el sistema est� listo conect�ndote al maestro y ejecutando <code>$ qstat -f</code>, obteniendo algo como: 

</p><p>
</p><pre>[root@maestro ~]$ qstat -f
queuename                      qtype resv/used/tot. load_avg arch          states
----------------------------------------------------------------------------
all.q@compute-0-0.local        BIP   0/4       0.00     lx26-x86
----------------------------------------------------------------------------
all.q@compute-0-1.local        BIP   0/4       0.00     lx26-x86
----------------------------------------------------------------------------
</pre>

<p>
Si alg�n nodo estuviera con problemas aparece en la columna <code>states</code> en el estado <code>au</code>.

</p><p>
</p></li>
<li> <i> C�mo ver qu� <span class="textit">rolls</span> est�n instalados  </i> 

<p>
Para este fin debes teclear en el terminal: <code>$ rocks list roll</code>

</p><p>
(en el apartado <a href="">0.2.2</a> se explica c�mo instalar un <span class="textit">roll</span>)

</p><p>
</p></li>
<li> <i> Nombres de los nodos  </i>

<p>
Por defecto, Rocks llama al nodo maestro <code>frontend</code>. 
Los nodos secundarios o <span class="textit">compute</span> se van numerando al crearse, 
desde <code>compute-0-0</code> hasta <code>compute-0-N</code>, donde N+1 es el n�mero 
total de nodos secundarios instalados. 

</p><p>
</p></li>
<li> <i> C�mo ver la carga de trabajo en el cluster  </i> <a name="top"></a>

<p>
Si quieres ver el estado actual de las colas de trabajos basta con teclear <code>$ qstat -f</code> en un terminal del maestro
y podr�s ver qu� est� corriendo en el cluster y qu� est� en espera, y la carga de cada nodo. 

</p><p>
Si quieres ver la carga global del sistema gr�ficamente lo mejor es usar el software 
<a name="tex2html17" href="http://ganglia.sourceforge.net/">ganglia</a>,
que suele estar instalado en los clusters 
<a name="tex2html18" href="http://www.rocksclusters.org/roll-documentation/ganglia/5.4/using-ganglia.html">Rocks</a>. 
Para ello abre un navegador web desde el nodo maestro apuntando a la URL 
<code>http://localhost/ganglia</code>, o si est� configurado el servidor web,
desde cualquier otra maquina apuntando a la URL 
<code>http://www.maestro.org/ganglia</code>. 

</p><p>

</p><div align="CENTER"><a name="fig:ganglia"></a><a name="166"></a>
<table>
<caption align="BOTTOM"><strong>Figura 2:</strong>
Estado de un cluster Rocks (de 16 nodos) tal como lo muestra Ganglia.</caption>
<tbody><tr><td>
<div align="CENTER">
<img width="800" height="600" align="BOTTOM" border="0" src="./Operaciones fundamentales para usuarios de un cluster Rocks_files/ganglia.png" alt="Image ganglia">

</div></td></tr>
</tbody></table>
</div>

<p>
</p></li>
<li> <i> C�mo conectarte a uno de los nodos secundarios  </i>

<p>
Por defecto, Rocks configura los nodos de manera que son parte de una red 
<a name="tex2html19" href="http://en.wikipedia.org/wiki/Local_area_network">LAN</a>
con el maestro e invisibles desde fuera de ella, 
as� que solamente podremos conectarnos a ellos desde un terminal del nodo maestro:
<code>root@maestro ~]# ssh compute-0-6</code>

</p><p>
que dependiendo de la versi�n de Rocks es equivalente a:

</p><p>
</p><pre>[root@cluster ~]$ ssh c0-6
</pre> 
<p>
</p></li>
<li> <i> C�mo probar el sistema de colas para distribuir tareas a los nodos  </i> <a name="SGE"></a>
<p>
En Rocks el manejador de colas por defecto es Grid Engine (SGE, incluido en el 
<a name="tex2html20" href="http://www.rocksclusters.org/roll-documentation/sge/5.4">roll sge</a>), 
que se explica por medio de ejemplos en la documentaci�n oficial
<a name="tex2html21" href="http://www.rocksclusters.org/roll-documentation/sge/5.4/submitting-batch-jobs.html">documentaci�n oficial</a>.

</p><p>
Vamos a probar que el SGE de nuestro cluster funciona, enviando una serie de trabajos sencillos al manejador
SGE mediante el comando <code>qsub</code>. Para ellos, primero editamos este c�digo y lo guardamos en un archivo 
llamado por ejemplo <code>testSGE.pl</code> :

</p><p>
</p><pre>#!/usr/bin/perl 

for(my $i=0;$i&lt;30;$i++){ sleep(2) }

print "ok!\n";
</pre>

<p>
Tras hacer el archivo ejecutable con <code>$ chmod +x testSGE.pl</code> podemos enviar varias instancias de este
programita al cluster y comprobar que los trabajos efectivamente se ejecutan haciendo:

</p><p>
</p><pre>[pepe@cluster ~]$ for ((i=1;i&lt;=10;i+=1)); do qsub testSGE.pl;  done
Your job 2 ("testSGE.pl") has been submitted
Your job 3 ("testSGE.pl") has been submitted
Your job 4 ("testSGE.pl") has been submitted
Your job 5 ("testSGE.pl") has been submitted
Your job 6 ("testSGE.pl") has been submitted
Your job 7 ("testSGE.pl") has been submitted
Your job 8 ("testSGE.pl") has been submitted
Your job 9 ("testSGE.pl") has been submitted
Your job 10 ("testSGE.pl") has been submitted
Your job 11 ("testSGE.pl") has been submitted

[root@cluster ~]$ qstat -f
queuename                      qtype resv/used/tot. load_avg arch          states
---------------------------------------------------------------------------------
all.q@compute-0-0.local        BIP   0/0/1          0.05     lx26-x86      

############################################################################
 - PENDING JOBS - PENDING JOBS - PENDING JOBS - PENDING JOBS - PENDING JOBS
############################################################################
      3 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1        
      4 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1        
      5 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1        
      6 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1        
      7 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1        
      8 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1        
      9 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1        
     10 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1        
     11 0.55500 testSGE.pl pepe         qw    06/10/2011 09:41:45     1
</pre>

<p>
Puedes indagar sobre todas las opciones de <code>qsub</code> en el terminal con <code>$ man qsub</code>,
por ejemplo para aprender a guardar los mensajes de error y la salida est�ndar en archivos,
como se muestra en el ejemplo <a href="">0.2.1</a>.

</p><p>
</p></li>
<li> <i> C�mo ejecutar el mismo comando en diferentes nodos del cluster desde el terminal  </i> <a name="fork"></a>
<p>
Es posible invocar comandos desde el <span class="textit">shell</span> del nodo maestro para que sean ejecutados 
en varios (o todos los) nodos usando la instrucci�n <code>rocks run host</code>, que sustituye al 
antiguo comando <code>cluster-fork</code>. Como es habitual en sistemas 
Linux, podemos consultar su forma de uso tecleando su nombre en el terminal:

</p><p>
</p><pre>[root@cluster ~]$ rocks run host   
error - must supply a command
[host]... {command} {managed} {x11} [command=string]
</pre>

<p>
Por ejemplo, para comprobar los procesos activos en todos los nodos
<span class="textit">compute</span> de un cluster, podemos teclear en el terminal: <code>$ rocks run host compute ps</code>

</p><p>
Ahora un ejemplo similar sobre un nodo en particular:
</p><pre>[root@cluster ~]$ rocks run host compute-0-0 "ls -l /tmp"
compute-0-1: total 12
compute-0-1: -rw-r--r-- 1 root root    0 Jun 14 09:28 post-91-sge-execd.debug
compute-0-1: -rw-r--r-- 1 root root    0 Jun 14 09:28 post-99-done.debug
compute-0-1: -rw-r--r-- 1 root root    0 Jun 14  2011 pre-09-prep-kernel-source.debug
compute-0-1: -rw-r--r-- 1 root root    0 Jun 14  2011 pre-10-src-install.debug
compute-0-1: drwx------ 2 root root 4096 Jun 14  2011 RCS
compute-0-1: -rw-r--r-- 1 root root 3321 Jun 14  2011 sshd_config
compute-0-1: drwx------ 2 root root 4096 Jun 14 09:42 ssh-qZwOne3375
</pre>

<p>
Otra manera de ejecutar un comando sobre un nodo es mediante SSH:
</p><pre>[pepe@maestro ~]$ ssh compute-0-3 df
Filesystem           1K-blocks      Used Available Use% Mounted on
/dev/sda1              8064272   5079996   2574624  67% /
none                   2052036         0   2052036   0% /dev/shm
/dev/sda5            140694608     93732 133453964   1% /state/partition1
/dev/sda2              4032124     93620   3733676   3% /var
maestro.local:/export/home/pepe
                     238299008   4739296 221454720   3% /home/pepe
</pre>		     

<p>
</p></li>
</ul>

<p>

</p><div class="navigation"><hr style="color:#66cc00">
<a name="tex2html87" href="">
<img align="BOTTOM" border="0" alt="previous" src="./Operaciones fundamentales para usuarios de un cluster Rocks_files/prev.png"></a> 
<a name="tex2html93" href="">
<img align="BOTTOM" border="0" alt="up" src="./Operaciones fundamentales para usuarios de un cluster Rocks_files/up.png"></a> 
<a name="tex2html95" href="">
<img align="BOTTOM" border="0" alt="next" src="./Operaciones fundamentales para usuarios de un cluster Rocks_files/next.png"></a> </div>
<!--End of Navigation Panel-->
<address>
<a href=""></a><br><br><a href=""></a>
</address>


</body></html>
