# P3. Tarefa DIG


### 1. Realiza unha consulta "dig danielcastelao.org" e identific cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER SECTION, AUTHORITY SECTION, etc)
Primero realizamos la consulta dig danielcastelao.org en nuestra terminal y después observamos lo que nos pone después de ese comando y analizamos la respuesta:
QUERY SECTION: Nos muestra el dominio de  danielcastelao.org y la consulta de tipo A.
ANSWER SECTION: Muestra las respuestas, que incluyen la IP 178.211.133.37 y el registro CNAME.
AUTHORITY SECTION: Indica el servidor autoritativo ns1.danielcastelao.org.
La etiqueta IN que aparece en la salida de dig significa Internet. Es parte de la clase de registro DNS que se está utilizando.
El Cname significa que el dominio danielcastelao.org es un alias o también puede  redireccionar a www.danielcastelao.org. 

### 2. Realiza consutas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org, www.danielcastelao.org  
Diferencias :

*moodle.danielcastealo.org*: No existe (NXDOMAIN), lo que indica que el dominio no fue encontrado, posiblemente por un error de escritura en el nombre del dominio.
*www.danielcastelao.org*: Existe (NOERROR) y se resolvió correctamente a una dirección IP.

moodle.danielcastealo.org: 171 ms (más lento, pero esto es común cuando se encuentra un error o no existe el dominio).
www.danielcastelao.org: 23 ms (respuesta rápida ) .
### 3. Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?
Primero ejecutamos dig danielcastelao.org NS para comprobar los nombres autoritativos una vez los tenemos porque nos los da ese comando pues ponemos los nombres con el comando dig ej : dig ns1danielcastelao.org
Ya ahí nos da las IPS en mi caso lo hice y me dio para el ns1 la ip 64.98.148.13 y la ns2 216.40.47.26
Os dominios suelen ser  polo menos dous servidores DNS autoritativos por:
  Redundancia: Se un falla, o outro garante a accesibilidade.
  Carga: Distribúen consultas para mellorar a resposta.
  Seguridade: Se un é atacado, o outro permanece operativo.
  Acceso Rexional: Redúcese a latencia.
  Mantenimiento: Permiten actualizacions sen interromper o servizo.

### 4. Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.
Realizamos a consulta con dig da ip 130.206.164.68 , na answer question aparecenos a ip 68.164.206.130 en inverso.
Despois realizamos a consulta 8.8.8.8 e aparecenos 
 ANSWER SECTION:
8.8.8.8.in-addr.arpa.  3600 IN PTR dns.google.
Realizamos outra consulta ca ip 1.1.1.1 e aparece : 
 ANSWER SECTION:
1.1.1.1.in-addr.arpa.  3600 IN PTR one.one.one.one.

### 5. A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?
para o 8.8.8.8 estamos consultando para google 
para 1.1.1.1 estamos consultando para Cloudflare

Podes cambiar temporalmente o servidor DNS que usas para consultas co comando dig ou  sen modificar os ficheiros de configuración. Simplemente temos que  especificar o servidor DNS que desexamos usar.

### 6. Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org.
Consultamos  ao servidor DNS de Google (8.8.8.8) executando dig @8.8.8.8 moodle.danielcastelao.org SOA. Despois, consulta ao servidor DNS primario de danielcastelao.org. Primeiro, obtén o servidor DNS primario executando dig danielcastelao.org NS e logo fai a consulta ao servidor primario (por exemplo, ns1.danielcastelao.org) executando dig @ns1.danielcastelao.org moodle.danielcastelao.org SOA. E así obtemos o rexistro SOA.

### 7. Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?
Primeiro, executamos o comando dig www.elpais.com para obter a IP do dominio. No resultado, buscamos a ANSWER SECTION, onde se mostra a dirección IP asociada.
A continuación, observamos o TTL (Time to Live) no resultado, que indica o tempo en segundos que o rexistro quedará almacenado no DNS local antes de expirar. Por exemplo, se vemos algo como www.elpais.com. 300 IN A 192.168.1.1, que e o meu caso que me apareceu que o rexistro se almacenará durante 300 segundos (5 minutos) no DNS local.

### 8. Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?
Vamos a elexir os dominios dos servicios de google amazon e facebook as diferencias que podemos ver ao lanzar o dig con estes servizos son : 
Os servizos que necesitan actualizaciones frecuentes poden ter un TTL máis baixo, mentres que os servizos estables (como os de almacenamento ou información estática) poden ter un TTL máis alto.
As empresas poden optar por diferentes políticas de caché en función da súa infraestrutura e necesidades de acceso.
Un TTL máis baixo pode reducir a latencia, pero tamén aumentar a carga sobre os servidores DNS.

### 9. Determina o TTL máximo (original) dun nome de dominio.
Para determinar o TTL máximo (orixinal) dun nome de dominio, segue estes pasos:

    Elixe un dominio: Escolla un dominio como www.example.com.

    Realiza a consulta: Executa o comando dig www.example.com.

    Busca o TTL: Na ANSWER SECTION, atoparás o valor do TTL, que indica canto tempo se almacenará o rexistro no caché DNS.

O TTL máximo varía, normalmente entre 3600 segundos (1 hora) e 86400 segundos (24 horas).

### 10. Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?

142.250.185.3 , 216.58.209.67 , 216.58.215.163 
As IPs (142.250.185.3, 216.58.209.67, 216.58.215.163) probablemente non sexan sempre as mesmas nin aparecerán sempre na mesma orde. Isto débese ao balanceo de carga a resposta aleatoria e tamén pode ser a optimización.
### 11. Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo
Para preguntar a un servidor raíz como J.ROOTSERVERS.NET e comprobar se acepta o modo recursivo o que facemos é: 
Primeiro, realiza a consulta ao servidor raíz usando o comando dig para preguntar por un dominio. Por exemplo, para consultar www.google.es ao servidor J.ROOTSERVERS.NET, executa o seguinte comando no terminal: dig www.google.es @J.ROOTSERVERS.NET. Despois, revisa a resposta que che devolve o comando e busca a sección que di flags. Finalmente, comproba se aparece a bandeira "ra" (Recursion Available), que indica se o servidor acepta consultas recursivas. Se non ves a bandeira ra, significa que o servidor non permite consultas recursivas, algo habitual nos servidores raíz, xa que estes normalmente só realizan consultas iterativas.

### 12. Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados

Para ver todas as consultas que fai o servidor DNS e averiguar a IP de www.timesonline.co.uk, usa o comando dig coa opción +trace, que mostra todo o camiño que segue a consulta a través dos servidores DNS. Primeiro, executa o seguinte comando no terminal: dig www.timesonline.co.uk +trace. Este comando mostrará todas as consultas que o servidor DNS realiza desde os servidores raíz ata os servidores autoritativos ata chegar á IP final. Ao final da saída, na ANSWER SECTION, verás a IP asociada a www.timesonline.co.uk, que será a resposta definitiva da consulta.

### 13. Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org
Debemos consultar os rexistros MX (Mail Exchange) a través do DNS. 
Executa a consulta: dig danielcastelao.org MX
Na ANSWER SECTION, atoparás os servidores de correo asociados ao dominio, xunto coa súa prioridade.
Para obter as IPs dos servidores listados, executa o comando dig para cada nome de servidor. 

### 14. Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?
Si que podes utilizando dig AAAA www.facebook.com.
Os rexistros AAAA de www.facebook.com corresponden a enderezos IP en formato IPv6.


