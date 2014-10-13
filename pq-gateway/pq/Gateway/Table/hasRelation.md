# bool pq\Gateway\Table::hasRelation(string $name[, string $table = NULL])

Check whether a relation to another table exists with the specified name.
See pq\Gateway\Table\Relations

> ***NOTE:***  
  The relation name is the column name of the foreign key with the column name of the referenced column cut off the end.

## Params:

* string $name  
  The name of the relation.
* Optional string $table = NULL  
  The bare table name, if the relation has another name (e.g. because of multiple foreign keys to the same table).

## Returns:

* bool, whether the specified relation exists.

## Example:

	<?php
	
	use pq\Gateway\Table;
	
	$conn = new pq\Connection;
	$conn->exec("
		drop table if exists account cascade;
		drop table if exists email cascade;
		drop table if exists reftable cascade;
		
		create table account (
			id serial primary key
		);
		
		create table email (
			id serial primary key,
			account_id integer references account(id),
			email text
		);
		
		create table reftable (
			id serial primary key,
			my_account integer references account(id),
			account_id integer references account(id),
			second_account_id integer references account(id),
			email integer references email(id)
		);
	");
	
	$fgn_table = new Table("reftable");
	var_dump($fgn_table->hasRelation("my_account"));
	
	?>

Yields:

	TRUE
