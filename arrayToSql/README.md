#Funcion para pasar un arreglo de datos y convertirlo a querys SQL#

##Funcionamiento##



###La funcion recibe 3 parametros###

La función sirve para evitar escribir una sentencia SQL completa,
la intencion es que al pasarle un array con los datos de la tabla, automaticamente
genere el query.

Solo sirve para funciones simples, no genera querys mas avanzados que tengan joins, o subconsultas anidadas.

>1. $type //El tipo de consulta (insert, delete, update, o select).
>2. $data //El array con los datos, los keys del array deben llamarse exactamente igual que los campos de la tabla.
>3. $table //El nombre de la tabla a la cual haremos nuestra consulta.

##Un ejemplo

<pre>
<code>
	/*
	 * Para un insert, creamos un array con los valores a insertar
	 */
	$data1 = array(
		'id' => 1,
		'campo1' => 'valor del campo uno',
		'campo2' => 'valor del campo dos',
		'campo3' => 'valor del campo tres'
	);
	$sql1 = arrayToSql('insert', $data1, 'tabla');
	//INSERT INTO tabla (id,campo1,campo2,campo3) VALUES('1','valor del campo uno','valor del campo dos','valor del campo tres');
	
	/*
	 * Para un update, se hace lo mismo, el id que llevara la condicional "WHERE" debe ir siempre al inicio del array
	 */
	$data2 = array(
		'id' => 1,
		'campo1' => 'nuevo valor del campo uno',
		'campo2' => 'nuevo valor del campo dos',
		'campo3' => 'nuevo valor del campo tres'
	);
	$sql2 = arrayToSql('update', $data2, 'tabla');
	//UPDATE tabla SET campo1='nuevo valor del campo uno', campo2='nuevo valor del campo dos', campo3='nuevo valor del campo tres' WHERE id = 1;
	
	/*
	 * Para un delete solo pasamos el id del registro a eliminar
	 */
	$data3 = array(
		'id' => 1
	);
	$sql3 = arrayToSql('delete', $data3, 'tabla');
	//DELETE FROM tabla WHERE id = 1;
	
	/*
	 * En un select el primer dato del array es el id de la condicional "WHERE", el segundo dato llamado "select"
	 * es un array con los campos a seleccionar de la tabla.
	 */	
	$data4 = array(
		'id' => 1,
		'select' => array('campo1','campo2','campo3')
	);
	$sql4 = arrayToSql('select', $data4, 'tabla');
	//SELECT campo1,campo2,campo3 FROM tabla WHERE id = 1;
</code>
</pre>

Post: [arrayToSql](http://cafeconweb.net/convertir-array-a-sql/ "Café Con Web") en mi blog.