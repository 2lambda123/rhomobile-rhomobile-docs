# RhoUtils API

Seed the Rhom database. For an example, see [Seeding the Database in Using the Local Database with Rhom](../rhodes/rhom#seeding-the-database).

## load_offline_data

Seed the Rhom database with initial data.

	:::ruby
	Rho::RhoUtils.load_offline_data(table_array, seed_prefix_directory)

<table border="1">
<tr>
	<td><code>table_array</code></td>
	<td>Array containing table names, which corresponds to pipe-delimited files.</td>
</tr>
<tr>
	<td><code>seed_prefix_directory</code></td>
	<td>Relative path to a directory containing a directory named fixtures, which contains the files listed in table_array.</td>
</tr>
</table>