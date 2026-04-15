<div id="popup-creation" style="display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: 9999; justify-content: center; align-items: center; padding: 20px;">
    
    <div onclick="document.getElementById('popup-creation').style.display='none'" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; background: rgba(10, 10, 15, 0.6); backdrop-filter: blur(15px); -webkit-backdrop-filter: blur(15px); transition: 0.5s;"></div>

    <div style="position: relative; padding: 50px; border-radius: 25px; text-align: center; color: white; font-family: 'Segoe UI', Roboto, sans-serif; max-width: 650px; overflow: hidden;
                /* EFFET GLACE LIQUIDE ICI */
                background: rgba(255, 255, 255, 0.03); /* Transparence légère */
                backdrop-filter: blur(25px) saturate(200%); /* Flou interne et couleurs saturées */
                -webkit-backdrop-filter: blur(25px) saturate(200%);
                border: 1px solid rgba(255, 255, 255, 0.12); /* Contour très fin effet verre */
                box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4), inset 0 0 15px rgba(255, 255, 255, 0.05); /* Ombres externe et interne pour le relief */
                transition: 0.4s ease-out; animation: popupSlideIn 0.6s ease-out;">
        
        <div style="position: absolute; top: -50%; left: -50%; width: 200%; height: 200%; background: radial-gradient(circle, rgba(255,255,255,0.08) 0%, rgba(255,255,255,0) 70%); pointer-events: none; transform: rotate(-30deg);"></div>

        <h1 style="color: #ffffff; margin-top: 0; font-size: 3em; font-weight: 900; text-transform: uppercase; letter-spacing: 2px; text-shadow: 0 0 15px rgba(255,255,255,0.5);">
            🚧 SITE EN COURS <br> DE CRÉATION
        </h1>
        
        <p style="font-size: 1.4em; margin: 30px 0 15px 0; font-weight: 500; color: rgba(255,255,255,0.9);">Bienvenue ! Ce site est actuellement en plein montage.</p>
        <p style="font-size: 1.2em; color: rgba(255,255,255,0.7); margin-bottom: 25px;">Certains liens peuvent ne pas fonctionner.</p>
        
        <p style="font-size: 1.2em; margin-top: 25px; font-weight: 500;">Merci de votre patience ! ✨</p>
        
        <button onclick="document.getElementById('popup-creation').style.display='none'" style="background: rgba(63, 81, 181, 0.3); color: white; border: 1px solid rgba(255,255,255,0.2); padding: 18px 50px; border-radius: 12px; cursor: pointer; font-weight: bold; font-size: 1.3em; margin-top: 35px; transition: 0.3s; backdrop-filter: blur(10px); text-transform: uppercase; letter-spacing: 1px; box-shadow: 0 5px 20px rgba(0,0,0,0.3);">
            J'AI COMPRIS !
        </button>
    </div>
</div>

<style>
    /* Petite animation d'entrée pour le style */
    @keyframes popupSlideIn {
        from { opacity: 0; transform: translateY(-50px) scale(0.95); }
        to { opacity: 1; transform: translateY(0) scale(1); }
    }
</style>

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
