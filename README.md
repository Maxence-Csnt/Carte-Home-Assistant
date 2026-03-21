> [!NOTE]
> Si vous utilisez le type d'affichage **Sections**, vous devrez peut-être définir la valeur `rows` à environ `1,5` pour la carte,
> sinon, la carte pourrait paraître déformée.
> (À UTILISER UNIQUEMENT EN CAS DE PROBLÈME).
>
> ```yaml
> grid_options:
>   rows: 1.5
> ```

>[!TIP]
>Vous souhaitez modifier la couleur des cartes et du texte (pratique pour ceux qui utilisent le mode clair) ? Ajoutez ce qui suit à `ha-card` et jouez avec les valeurs (rgb, hex, etc.).
>
```yaml
background: #1C1C1C !important;
--card-primary-color: white !important;
--card-secondary-color: white !important;
```
<hr>
