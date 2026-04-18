# Carte Incendie 🔥

<img width="465" height="552" alt="Incendie" src="https://github.com/user-attachments/assets/567942fb-a63d-4282-ba88-02b3d900fbd8" />

Voici le code à copier dans ton automatisation Home Assistant :

```yaml
#——————————————————
# Crée par Maxence_Csnt
# Carte Incendie
# Support : https://discord.gg/s6cZ7Swhh7
#——————————————————

type: custom:button-card
entity: input_boolean.alarme_active
name: ALERTE INCENDIE
icon: mdi:fire
aspect_ratio: 1/1.2
show_state: false
tap_action:
  action: none
hold_action:
  action: none
styles:
  grid:
    - grid-template-areas: "\"i\" \"n\" \"danger\" \"emergency\" \"button\""
    - grid-template-rows: 1fr auto auto auto auto
  card:
    - background-color: "#1a0a0a"
    - border: "2px solid #ff4d4d"
    - border-radius: 25px
    - padding: 10% 5%
    - cursor: default
  icon:
    - color: "#ff4d4d"
    - width: 125px
    - filter: "drop-shadow(0 0 12px #ff4d4d)"
    - animation: blink 1s ease-in-out infinite
    - pointer-events: none
  name:
    - color: "#ff4d4d"
    - font-weight: 900
    - font-size: 26px
    - margin-bottom: 5px
    - pointer-events: none
  custom_fields:
    danger:
      - pointer-events: none
    emergency:
      - pointer-events: none
extra_styles: |
  @keyframes blink {
    0% { opacity: 1; filter: drop-shadow(0 0 12px #ff4d4d); }
    50% { opacity: 0.3; filter: drop-shadow(0 0 0px #ff4d4d); }
    100% { opacity: 1; filter: drop-shadow(0 0 12px #ff4d4d); }
  }
custom_fields:
  danger: |
    [[[ 
      const detecteurs = [
        'binary_sensor.etat_de_la_fumee_couloir_bas',
        'binary_sensor.etat_de_la_fumee_couloir_haut',
        'binary_sensor.etat_de_la_fumee_arriere_cuisine',
        'binary_sensor.etat_de_la_fumee_sejour',
        'binary_sensor.etat_de_la_fumee_vmc',
        'binary_sensor.etat_de_la_fumee_garage'
      ];
      const actif = detecteurs.find(d => states[d] && states[d].state === 'on');
      const nomDetecteur = actif ? states[actif].attributes.friendly_name : "Déclencheur de Test";
      return `
        <div style="color: #888; font-size: 14px; text-transform: uppercase;">Danger détecté par :</div>
        <div style="color: #fff; font-weight: bold; font-size: 18px; margin-bottom: 15px;">
          ${nomDetecteur}
        </div>
      `;
    ]]]
  emergency: |
    [[[ 
      return `
        <div style="background: #2a1515; padding: 20px; border-radius: 15px; border: 1px solid #ff4d4d66; margin-bottom: 20px;">
          <div style="color: #ffcc00; font-weight: bold; font-size: 16px;">⚠️ ÉVACUATION IMMÉDIATE ⚠️</div>
          <div style="color: #888; font-size: 12px; margin: 5px 0;">Appelez les secours</div>
          <div style="font-size: 45px; color: #fff; font-weight: bold; line-height: 1;">18</div>
        </div>
      `
    ]]]
  button:
    card:
      type: custom:button-card
      name: ARRÊTER L' ALERTE
      tap_action:
        action: browser_mod.close_popup
        data: {}
      styles:
        card:
          - background-color: "#ff4d4d"
          - border-radius: 30px
          - height: 50px
        name:
          - color: white
          - font-weight: bold
          - font-size: 14px
```
