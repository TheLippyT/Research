Syncfusion Grid Localization

Issues:

- [x] too much locale boilerplate code find a way to make it more efficient

Changes:

added locale for the ej2 components

- ```Angular
      setCulture('nl-NL');
      
      L10n.load({
        'nl-NL':{
          grid:{
            Add: 'Toevoegen',
            Edit: 'Bewerken',
            Delete: 'Wissen',
            Update: 'Wijzigen',
            Cancel: 'Annuleren',
            EmptyRecord: 'Er is geen data beschikbaar',
            EditOperationAlert: 'Geen data geselecteerd voor bewerking'
          }
        }
      });
      
      public readonly locale: string = 'nl-NL';
    ```