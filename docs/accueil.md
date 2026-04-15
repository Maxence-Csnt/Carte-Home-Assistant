<div id="popup-creation" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); z-index: 9999; justify-content: center; align-items: center;">
    <div style="background: #1a1a1a; padding: 30px; border-radius: 15px; border: 2px solid #3f51b5; max-width: 500px; text-align: center; color: white; box-shadow: 0 0 20px rgba(0,0,0,0.5);">
        <h2 style="color: #3f51b5; margin-top: 0;">🚧 Site en cours de création</h2>
        <p>Bienvenue ! Ce site est actuellement en plein montage. Certains liens peuvent ne pas fonctionner.</p>
        <p>Merci de votre patience ! ✨</p>
        <button onclick="document.getElementById('popup-creation').style.display='none'" style="background: #3f51b5; color: white; border: none; padding: 10px 25px; border-radius: 5px; cursor: pointer; font-weight: bold; margin-top: 15px;">D'accord, j'ai compris !</button>
    </div>
</div>

<script>
    // Affiche le popup au chargement de la page
    window.onload = function() {
        document.getElementById('popup-creation').style.display = 'flex';
    };
</script>


---

!!! danger "Site en cours de construction 🏗️"
    Ce site est actuellement en **plein développement**. Certains liens ou images peuvent être manquants.  
    Merci de votre patience ! ✨


!!! warning "Besoin d'un coup de main ?"
    **Rejoignez-nous directement sur le Discord de Glooob Domo !**
    **[Clique ici pour rejoindre le Discord](https://discord.gg/8w5kVPHeEY)**

---

!!! note "Affichage en mode Sections"
    Si vous utilisez le type d'affichage **Sections**, vous devrez peut-être définir la valeur `rows` à environ `1.5` pour la carte.
    
    ```yaml
    grid_options:
      rows: 1.5
    ```

!!! tip "Personnalisation des couleurs"
    Ajoutez ce bloc dans la partie `ha-card` :

    ```css
    background: #1C1C1C !important;
    --card-primary-color: white !important;
    --card-secondary-color: white !important;
    ```
---
