# mixed pq\Gateway\Table::by(pq\Gateway\Row $me, string $foreign[, $order = NULL[, int $limit = 0[, int $offset = 0]]])

Find rows in another table by foreign key.
See pq\Gateway\Table::find(), pq\Gateway\Table::of() and pq\Gateway\Row::ofWhich().

## Params:

* pq\Gateway\Row $row  
  A row of this table referenced by another table through a foreign key.
* Optional string $name = NULL  
  The identifying name of the relation.
* Optional string $order = NULL  
  Sorting clause.
* Optional int $limit = 0  
  Row count limit.
* Optional int $offset = 0  
  Row count offset.

## Returns:

* a [deferred promise of React/Promise](https://github.com/reactphp/promise#deferred-1), when using pq\Query\AsyncExecutor, the asynchronous executor.  
  Else:
* pq\Result, if pq\Result::$status != pq\Result::TUPLES_OK.
* pq\Result, if the rowset prototype pq\Gateway\Table::$rowset is empty.
* pq\Gateway\Rowset, an instance of the rowset prototype.

## Example:

	<?php
	
	use pq\Gateway\Table;
	
	$account_emails = new Table("account_emails");
	$email = $account_emails->find(["email=" => "mike@php.net"])->current();
	
	$account = $account_emails->by($email, "account")->current();
	
	?>
