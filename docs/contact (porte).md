# Carte Contact 🚪 (Porte)

<img width="536" height="84" alt="Porte" src="https://github.com/user-attachments/assets/49d2f95a-8f9d-48cf-ad95-fa33b1ec0398" />

Voici le code à copier dans ton dashboard Home Assistant :
```yaml
#——————————————————
# Crée par Anas Box modifier par Maxence_Csnt
# Carte Contact (Porte)
# Support : https://discord.gg/s6cZ7Swhh7
#——————————————————

type: custom:mushroom-entity-card
entity: binary_sensor.porte_d_entree_contact
tap_action:
  action: more-info
icon: ""
primary_info: state
secondary_info: name
grid_options:
  columns: 12
  rows: 1
icon_color: red
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {% set is_open = is_state(config.entity, 'on') %}

        /* LOGIC: Define colors and animations based on state */
        {% if is_open %}
            /* OPEN: Red, Dark Red Shape, Animated */
            --icon-color-set: rgb(244, 67, 54);
            --shape-color-set: rgba(160, 0, 0, 0.15); 
            --shape-animation: door-soft-open 1.7s ease-in-out infinite;
            --glow-animation: door-soft-glow-red 2.5s ease-in-out infinite;
            --beam-animation: door-soft-beam-red 2.5s ease-in-out infinite;
            --icon-filter: drop-shadow(0 0 6px rgba(160, 0, 0, 0.95));
        {% else %}
            /* CLOSED: Green, Glow & Beam Animations active */
            --icon-color-set: rgb(76, 175, 80);
            --shape-color-set: rgba(0, 100, 0, 0.15);
            --shape-animation: none;
            --glow-animation: door-soft-glow-green 5s ease-in-out infinite;
            --beam-animation: door-soft-beam-green 5s ease-in-out infinite;
            --icon-filter: drop-shadow(0 0 6px rgba(0, 119, 0, 0.95));
        {% endif %}

        background-color: var(--shape-color-set) !important;
        position: relative;
        transform-origin: 25% 50%;
        animation: var(--shape-animation);
      }

      .shape ha-icon {
        color: var(--icon-color-set) !important;
        filter: var(--icon-filter);
      }

      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      /* Inner Glow */
      .shape::before {
        inset: -10px;
        animation: var(--glow-animation);
      }

      /* Outer Beam */
      .shape::after {
        inset: -15px;
        animation: var(--beam-animation);
        mix-blend-mode: screen;
      }

      /* --- KEYFRAMES RED --- */
      @keyframes door-soft-glow-red {
        0%, 100% { box-shadow: 0 0 20px 0 rgba(160, 0, 0, 0.7), 0 0 40px 6px rgba(160, 0, 0, 0.6); }
        50% { box-shadow: 0 0 30px 4px rgba(200, 0, 0, 1), 0 0 70px 16px rgba(200, 0, 0, 0.95); }
      }
      @keyframes door-soft-beam-red {
        0%, 100% { box-shadow: 0 0 40px 10px rgba(160, 0, 0, 0.3); opacity: 0.4; }
        50% { box-shadow: 0 0 160px 60px rgba(230, 20, 20, 0.8); opacity: 1; }
      }

      /* --- KEYFRAMES GREEN --- */
      @keyframes door-soft-glow-green {
        0%, 100% { box-shadow: 0 0 20px 0 rgba(0, 160, 0, 0.7), 0 0 40px 6px rgba(0, 160, 0, 0.6); }
        50% { box-shadow: 0 0 30px 4px rgba(0, 200, 0, 1), 0 0 70px 16px rgba(0, 200, 0, 0.95); }
      }
      @keyframes door-soft-beam-green {
        0%, 100% { box-shadow: 0 0 40px 10px rgba(0, 160, 0, 0.3); opacity: 0.4; }
        50% { box-shadow: 0 0 160px 60px rgba(20, 230, 20, 0.8); opacity: 1; }
      }

      @keyframes door-soft-open {
        0% { transform: rotate(0deg); }
        40% { transform: rotate(-9deg); }
        70% { transform: rotate(-6deg); }
        100% { transform: rotate(0deg); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 25px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
      }
```
