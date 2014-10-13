# \pq\Gateway\Table\Relations|stdClass pq\Gateway\Table::getRelations([string $to = NULL])

Get the relations (by foreign key) of this table.
See pq\Gateway\Table::hasRelation().

> ***NOTE:***  
  The relation name is the column name of the foreign key with the column name of the referenced column cut off the end.

## Params:

* Optional string $to = NULL  
  The table name of which to get the relation to.

## Returns:

* stdClass, if $to is given and a relation exists.
* NULL, if $to is given and a relation does not exist.
* pq\Gateway\Table\Relations, all relations if $to is omitted.

## Example:

	<?php
	
	use pq\Gateway\Table;
	
	$conn = new pq\Connection;
	$conn->exec("
		drop table if exists reftable cascade;
		-- drop table if exists account cascade;
		-- drop table if exists account_email cascade;

		-- create table account (
		-- 	id uuid default uuid_generate_v4() primary key,
		-- 	password char(60),
		-- 	name varchar(68)
		-- );

		-- create table account_email (
		-- 	account_id uuid not null references account(id) on delete cascade,
		-- 	email varchar(255) not null unique,
		-- 	primary key (account_id, email)
		-- );
		
		create table reftable (
			id serial primary key,
			my_account integer references account(id),
			account_id integer references account(id),
			second_account_id integer references account(id),
			email integer references account_email(email)
		);
	");
	
	$fgn_table = new Table("reftable");
	var_dump($fgn_table->getRelations());
	
	?>

Yields:

	object(pq\Gateway\Table\Relations)#10 (1) {
	  ["references":protected]=>
	  object(stdClass)#17 (4) {
		["my_account"]=>
		object(stdClass)#18 (1) {
		  ["reftable"]=>
		  object(stdClass)#19 (4) {
			["foreignTable"]=>
			string(8) "reftable"
			["foreignColumn"]=>
			string(10) "my_account"
			["referencedTable"]=>
			string(7) "account"
			["referencedColumn"]=>
			string(2) "id"
		  }
		}
		["account"]=>
		object(stdClass)#20 (1) {
		  ["reftable"]=>
		  object(stdClass)#21 (4) {
			["foreignTable"]=>
			string(8) "reftable"
			["foreignColumn"]=>
			string(10) "account_id"
			["referencedTable"]=>
			string(7) "account"
			["referencedColumn"]=>
			string(2) "id"
		  }
		}
		["second_account"]=>
		object(stdClass)#22 (1) {
		  ["reftable"]=>
		  object(stdClass)#23 (4) {
			["foreignTable"]=>
			string(8) "reftable"
			["foreignColumn"]=>
			string(17) "second_account_id"
			["referencedTable"]=>
			string(7) "account"
			["referencedColumn"]=>
			string(2) "id"
		  }
		}
		["email"]=>
		object(stdClass)#24 (1) {
		  ["reftable"]=>
		  object(stdClass)#25 (4) {
			["foreignTable"]=>
			string(8) "reftable"
			["foreignColumn"]=>
			string(5) "email"
			["referencedTable"]=>
			string(13) "account_email"
			["referencedColumn"]=>
			string(5) "email"
		  }
		}
	  }
	}
