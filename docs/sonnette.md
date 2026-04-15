# Carte Sonnette 🔔

<img width="526" height="91" alt="Sonnette" src="https://github.com/user-attachments/assets/128227c6-b32b-4c99-8603-c82e20352210" />

Voici le code à copier dans ton dashboard Home Assistant :

```yaml
#——————————————————
# Crée par Anas Box modifier par Maxence_Csnt
# Carte Sonnette
# Support : https://discord.gg/s6cZ7Swhh7
#——————————————————

type: custom:mushroom-entity-card
entity: binary_sensor.portail_visiteur
icon: mdi:bell
icon_color: red
name: Sonnette
grid_options:
  columns: 12
  rows: 1.25
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== USER CONFIG ========== #}
        {# true = number mode, false = state mode #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'switch.plug_6_local' %}
        {% set active_value    = 'on' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        
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
          {# default: simple equality state trigger #}
          {% set trigger_active = (states(state_entity) == active_value) %}
        {% endif %}
        {# =========== END TRIGGER LOGIC =========== #}


        {% if trigger_active %}
          --shape-animation: doorbell-ring 0.9s ease-out infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          opacity: 0.8;
        {% endif %}

        transform-origin: 50% 50%;
      }

      @keyframes doorbell-ring {
        0% {
          transform: scale(1.05);
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 1),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.8),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        30% {
          transform: scale(0.95);
          box-shadow:
            0 0 0 4px  rgba(var(--rgb-{{ config.icon_color }}), 0.9),
            0 0 0 10px rgba(var(--rgb-{{ config.icon_color }}), 0.7),
            0 0 0 18px rgba(var(--rgb-{{ config.icon_color }}), 0.4);
        }
        60% {
          transform: scale(1.02);
          box-shadow:
            0 0 0 10px rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 18px rgba(var(--rgb-{{ config.icon_color }}), 0.2),
            0 0 0 26px rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
        100% {
          transform: scale(1);
          box-shadow:
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0),
            0 0 0 0 rgba(var(--rgb-{{ config.icon_color }}), 0.0);
        }
      }

      @keyframes doorbell-idle {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(1); }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }
```
