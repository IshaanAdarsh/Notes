# Model Operations

1. **CreateModel**: Creates a new model in the project history and a corresponding table in the database with specified fields, options, bases, and managers.
2. **DeleteModel**: Deletes the model from the project history and its table from the database.
3. **RenameModel**: Renames the model from an old name to a new one, handling data migration if required.
4. **AlterModelTable**: Changes the model's table name defined in the Meta subclass.
5. **AlterUniqueTogether**: Modifies the model's set of unique constraints defined in the Meta subclass.
6. **AlterIndexTogether**: Adjusts the model's set of custom indexes specified in the Meta subclass.
7. **AlterOrderWithRespectTo**: Adds or removes the _order column required for the order with respect to option in the Meta subclass.
8. **AlterModelOptions**: Stores changes to miscellaneous model options (permissions, verbose name) in the Meta subclass for future use.
9. **AlterModelManagers**: Alters the managers available during migrations for the model.
10. **AddField**: Adds a new field to the model with specified name and field definition, optionally preserving default values.
11. **RemoveField**: Removes a field from the model, making the operation reversible if the field is nullable or has a default value.
12. **AlterField**: Alters a field's definition, including changes to its type, nullability, uniqueness, and other attributes.
13. **RenameField**: Changes a field's name and, if the column is not set, the column name as well.
14. **AddIndex**: Creates an index for the model in the database with specified index configuration.
15. **RemoveIndex**: Removes a specific index from the model's database table.
16. **AddConstraint**: Creates a constraint for the model in the database with specified constraints.
17. **RemoveConstraint**: Removes a specific constraint from the model's database table.
