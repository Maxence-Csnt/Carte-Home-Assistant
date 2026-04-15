# Carte Détecteur de mouvement 💨

<img width="516" height="97" alt="Détecteur de mouvement" src="https://github.com/user-attachments/assets/2ee821d1-feb7-4467-bef5-cd7270f13d76" />

Voici le code à copier dans ton dashboard Home Assistant :

```yaml
#——————————————————
# Crée par Anas Box modifier par Maxence_Csnt
# Carte Détecteur de mouvement
# Support : https://discord.gg/s6cZ7Swhh7
#——————————————————

type: custom:mushroom-entity-card
entity: binary_sensor.detecteur_de_mouvement_occupancy
tap_action:
  action: none
icon: mdi:motion-sensor
icon_color: red
grid_options:
  columns: 12
  rows: 1.25
primary_info: state
secondary_info: name
hold_action:
  action: none
double_tap_action:
  action: none
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'binary_sensor.detecteur_de_mouvement_occupancy' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'binary_sensor.detecteur_de_mouvement_occupancy' %}
        
        {# '>' '<' '=' '>=' '<=' #}
        {% set number_operator = '>' %}
        
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ======== TRIGGER DECISION LOGIC ======== #}
        {% if use_number %}
          {% set num = states(number_entity) | float(0) %}

          {% if number_operator == '>' %}
            {% set trigger_active = (num > threshold) %}
          {% elif number_operator == '<' %}
            {% set trigger_active = (num < threshold) %}
          {% elif number_operator == '=' %}
            {% set trigger_active = (num == threshold) %}
          {% elif number_operator == '>=' %}
            {% set trigger_active = (num >= threshold) %}
          {% elif number_operator == '<=' %}
            {% set trigger_active = (num <= threshold) %}
          {% else %}
            {% set trigger_active = false %}
          {% endif %}
        {% else %}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}

        {% if trigger_active %}
          --shape-animation: motion-active 1.4s linear infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.7;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes motion-active {
        0% {
          transform: scale(1);
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        40% {
          transform: scale(1.06);
          box-shadow:
            0 0 0 6px rgba(var(--rgb-{{ config.icon_color }}), 0.5),
            0 0 0 12px rgba(var(--rgb-{{ config.icon_color }}), 0.2);
        }
        100% {
          transform: scale(1);
          box-shadow:
            0 0 0 16px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 24px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
      }

      @keyframes motion-scan {
        0% {
          transform: rotate(0deg);
          box-shadow:
            0 -10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9);
        }
        50% {
          transform: rotate(180deg);
          box-shadow:
            0 10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.6);
        }
        100% {
          transform: rotate(360deg);
          box-shadow:
            0 -10px 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.9);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -15px 0 10px -18px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }
```
