# pq\Query\WriterInterface pq\Query\WriterInterface::criteria(array $criteria)

Write nested AND/OR criteria to the query string.

## Params:

* array $criteria  
  Nested AND/OR criteria.

## Returns:

* pq\Query\WriterInterface, self.

## Example:

	<?php
	
	use pq\Query;
	
	$q = new Query\Writer;
	$q->write("select * from account where")
	  ->criteria([
	    ["id >" => 1, "id <" => 5],
	    ["name =" => "mike"]
	  ]);
	
	var_dump((string) $q, $q->getParams());
	
	?>

Yields:

	string(84) "select * from account where ( ( ( id > $1 ) AND ( id < $2 ) ) OR ( ( name = $3 ) ) )"
	array(3) {
	  [0]=>
	  int(1)
	  [1]=>
	  int(5)
	  [2]=>
	  string(4) "mike"
	}
