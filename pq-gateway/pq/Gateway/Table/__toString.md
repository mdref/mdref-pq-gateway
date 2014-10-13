# string pq\Gateway\Table::__toString()

Format an identifying postgresql:// URL.

## Params:

None.

## Returns:

* string, the formatted URL.

## Example:

	<?php
	
	echo new pq\Gateway\Table("account",
		new pq\Connection("application_name='pq-gateway-docs' connect_timeout=10"));
	
	?>

Yields:

	postgresql://mike:@:5432/mike?#account
