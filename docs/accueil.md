<div id="popup-creation" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); z-index: 9999; justify-content: center; align-items: center; padding: 20px;">
    <div style="background: #1a1a1a; padding: 40px; border-radius: 20px; border: 3px solid #3f51b5; max-width: 600px; text-align: center; color: white; box-shadow: 0 0 30px rgba(0,0,0,0.7);">
        
        <h1 style="color: #3f51b5; margin-top: 0; font-size: 2.5em; font-weight: 900; line-height: 1.2;">
            🚧 SITE EN COURS <br> DE CRÉATION
        </h1>
        
        <p style="font-size: 1.2em; margin-top: 20px;">Bienvenue ! Ce site est actuellement en plein montage. Certains liens peuvent ne pas fonctionner.</p>
        <p style="font-size: 1.1em; color: #bbb;">Merci de votre patience ! ✨</p>
        
        <button onclick="document.getElementById('popup-creation').style.display='none'" style="background: #3f51b5; color: white; border: none; padding: 15px 35px; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 1.1em; margin-top: 25px; transition: 0.3s;">
            D'ACCORD, J'AI COMPRIS !
        </button>
    </div>
</div>

<script>
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
