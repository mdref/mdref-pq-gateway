# stdClass pq\Gateway\Table\Relations::getReference(string $to)

Retrieve the foreign key of the table to another table.

## Params:

* string $to  
  The table name referenced by a foreign key of the table.

## Returns:

* stdClass, the table relation.
* NULL, if the tables are not related.

## Example:

	<?php
	
	use pq\Gateway\Table;
	
	$email = new Table("account_email");
	$relation = new Table\Relations($email);
	$account = $relation->getReference("account");
	
	var_dump($account);
	
	?>

Yields:

	object(stdClass)#13 (1) {
	  ["account_email"]=>
	  object(stdClass)#14 (4) {
		["foreignTable"]=>
		string(13) "account_email"
		["foreignColumn"]=>
		string(10) "account_id"
		["referencedTable"]=>
		string(7) "account"
		["referencedColumn"]=>
		string(2) "id"
	  }
	}

