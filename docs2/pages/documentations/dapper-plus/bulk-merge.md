# Dapper Plus - Bulk Merge

## Description
MERGE entities using Bulk Operation.

- [Merge single](#example---merge-single)
- [Merge many](#example---merge-many)
- [Merge with relation (One to One)](#example---merge-with-relation-one-to-one)
- [Merge with relation (One to Many)](#example---merge-with-relation-one-to-many)

## Example - Merge Single
MERGE a single entity with Bulk Operation.

```csharp
using (var connection = My.ConnectionFactory())
{
    connection.Open();

    connection.BulkMerge(invoice);
}
```

## Example - Merge Many
MERGE many entities with Bulk Operation.

```csharp
using (var connection = My.ConnectionFactory())
{
    connection.Open();

    connection.BulkMerge(invoices);
}
```

## Example - Merge with relation (One to One)
MERGE entities with a one to one relation with Bulk Operation.

```csharp
using (var connection = My.ConnectionFactory())
{
    connection.Open();

	connection.BulkMerge(invoices)
		.ThenForEach(x => x.Detail.InvoiceID = x.InvoiceID)
		.ThenBulkMerge(x => x.Detail);
}
```

## Example - Merge with relation (One to Many)
MERGE entities with a one to many relation with Bulk Operation.

```csharp
using (var connection = My.ConnectionFactory())
{
    connection.Open();

	connection.BulkMerge(invoices)
		.ThenForEach(x => x.Items.ForEach(y => y.InvoiceID = x.InvoiceID))
		.ThenBulkMerge(x => x.Items);
}
```