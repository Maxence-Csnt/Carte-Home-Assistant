---
hide:
  - navigation
  - toc
search:
  boost: 5.0
---

# 84291

### 🔐 Contenu Spéciale
Vous avez déverrouillé l'accès à la configuration

---

Bonjour ThGraf,
Voici le code à copier : 
Dans ton dashboard cree une carte `Manuel` puis coller le code ci-dessou :

## Chauffages :
> ### ⚡ ACCÈS DIRECT AU CODE
> [Thermostat](#thermostat) | [RAD - CH1](#rad-ch1) | [RAD - CH2](#rad-ch2) | [RAD - CH3](#rad-ch3) | [RAD - CH4](#rad-ch4) | [RAD - CH5](#rad-ch5) |

## A/C :
> ### ⚡ ACCÈS DIRECT AU CODE
> [A/C - Véranda](#ac-veranda) | [A/C - CH1](#ac-ch1) | [A/C - CH2](#ac-ch2) | [A/C - CH3](#ac-ch3) | [A/C - CH4](#ac-ch4) | [A/C - CH5](#ac-ch5) |

---

### Thermostat {: #thermostat }
```yaml
# Thermostat
type: custom:mushroom-climate-card
entity: climate.rad_thermostatprincipal
collapsible_controls: false
show_temperature_control: true
fill_container: false
hvac_modes:
  - Off
  - Planning #(ou mode par défaut)
  - Absent
  - Hors Gel
  - Boost
name: Thermostat
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========= FLAME COLOR CONFIG ========= #}
        {% set flame_color = 'deep-orange' %}   {# 'red', 'amber', 'orange', etc. #}
        --flame-color-rgb: var(--rgb-{{ flame_color }});
        {# ===================================== #}

        {# ========== USER CONFIG ========== #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'climate.heatpump' %}
        {% set active_value    = 'heat' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ----------- TRIGGER LOGIC ----------- #}
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
        {# --------- END TRIGGER LOGIC --------- #}

        {% if trigger_active %}
          # --shape-animation: flame-core 1.4s infinite;
          --flame-layer1: flame-layers 1.8s infinite;
          --flame-layer2: ember-pulse 2.4s infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --flame-layer1: none;
          --flame-layer2: none;
          opacity: 0.6;
        {% endif %}

        position: relative;
        transform-origin: 50% 75%;
      }

      /* Flame layers */
      .shape::before,
      .shape::after {
        content: "";
        position: absolute;
        inset: -8px;
        border-radius: inherit;
        pointer-events: none;
        filter: blur(3px);
      }

      .shape::before {
        animation: var(--flame-layer1);
      }

      .shape::after {
        animation: var(--flame-layer2);
      }

      /* Core flame motion: chaotic vertical flicker + heat ripple */
      @keyframes flame-core {
        0%   { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
        12%  { transform: translateY(-2px) scale(1.05);  filter: brightness(1.4) hue-rotate(-10deg); }
        25%  { transform: translateY(1px)  scale(0.98);  filter: brightness(0.9) hue-rotate(8deg); }
        40%  { transform: translateY(-3px) scale(1.07);  filter: brightness(1.5) hue-rotate(-18deg); }
        55%  { transform: translateY(0)    scale(1.02);  filter: brightness(1.2) hue-rotate(10deg); }
        70%  { transform: translateY(-1px) scale(1.04);  filter: brightness(1.35) hue-rotate(-6deg); }
        85%  { transform: translateY(2px)  scale(0.97);  filter: brightness(0.95) hue-rotate(6deg); }
        100% { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
      }

      /* Outer flame shape: shifting blurred glow */
      @keyframes flame-layers {
        0% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
        33% {
          box-shadow:
            0 0 20px 10px rgba(var(--flame-color-rgb), 1),
            0 -16px 30px -8px rgba(255, 160, 0, 0.5);
        }
        66% {
          box-shadow:
            0 0 18px 9px rgba(var(--flame-color-rgb), 0.9),
            0 -8px 20px -6px rgba(255, 220, 0, 0.35);
        }
        100% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
      }

      /* Ember pulse: slow breathing glow */
      @keyframes ember-pulse {
        0% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
        50% {
          box-shadow:
            0 0 50px 18px rgba(var(--flame-color-rgb), 0.5),
            0 0 90px 35px rgba(255, 150, 0, 0.25);
        }
        100% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -17px 0 20px -17px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }
grid_options:
  columns: 6
  rows: 2
```

---

### RAD - CH1 {: #rad-ch1 }
```yaml
# RAD - CH1
type: custom:mushroom-climate-card
entity: climate.rad_ch1
collapsible_controls: false
show_temperature_control: true
fill_container: false
hvac_modes:
  - auto
  - heat_cool
  - cool
  - heat
  - dry
  - fan_only
  - "off"
name: RAD - CH1
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========= FLAME COLOR CONFIG ========= #}
        {% set flame_color = 'deep-orange' %}   {# 'red', 'amber', 'orange', etc. #}
        --flame-color-rgb: var(--rgb-{{ flame_color }});
        {# ===================================== #}

        {# ========== USER CONFIG ========== #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'climate.heatpump' %}
        {% set active_value    = 'heat' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ----------- TRIGGER LOGIC ----------- #}
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
        {# --------- END TRIGGER LOGIC --------- #}

        {% if trigger_active %}
          # --shape-animation: flame-core 1.4s infinite;
          --flame-layer1: flame-layers 1.8s infinite;
          --flame-layer2: ember-pulse 2.4s infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --flame-layer1: none;
          --flame-layer2: none;
          opacity: 0.6;
        {% endif %}

        position: relative;
        transform-origin: 50% 75%;
      }

      /* Flame layers */
      .shape::before,
      .shape::after {
        content: "";
        position: absolute;
        inset: -8px;
        border-radius: inherit;
        pointer-events: none;
        filter: blur(3px);
      }

      .shape::before {
        animation: var(--flame-layer1);
      }

      .shape::after {
        animation: var(--flame-layer2);
      }

      /* Core flame motion: chaotic vertical flicker + heat ripple */
      @keyframes flame-core {
        0%   { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
        12%  { transform: translateY(-2px) scale(1.05);  filter: brightness(1.4) hue-rotate(-10deg); }
        25%  { transform: translateY(1px)  scale(0.98);  filter: brightness(0.9) hue-rotate(8deg); }
        40%  { transform: translateY(-3px) scale(1.07);  filter: brightness(1.5) hue-rotate(-18deg); }
        55%  { transform: translateY(0)    scale(1.02);  filter: brightness(1.2) hue-rotate(10deg); }
        70%  { transform: translateY(-1px) scale(1.04);  filter: brightness(1.35) hue-rotate(-6deg); }
        85%  { transform: translateY(2px)  scale(0.97);  filter: brightness(0.95) hue-rotate(6deg); }
        100% { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
      }

      /* Outer flame shape: shifting blurred glow */
      @keyframes flame-layers {
        0% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
        33% {
          box-shadow:
            0 0 20px 10px rgba(var(--flame-color-rgb), 1),
            0 -16px 30px -8px rgba(255, 160, 0, 0.5);
        }
        66% {
          box-shadow:
            0 0 18px 9px rgba(var(--flame-color-rgb), 0.9),
            0 -8px 20px -6px rgba(255, 220, 0, 0.35);
        }
        100% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
      }

      /* Ember pulse: slow breathing glow */
      @keyframes ember-pulse {
        0% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
        50% {
          box-shadow:
            0 0 50px 18px rgba(var(--flame-color-rgb), 0.5),
            0 0 90px 35px rgba(255, 150, 0, 0.25);
        }
        100% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -17px 0 20px -17px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }
grid_options:
  columns: 6
  rows: 2
```

---

### RAD - CH2 {: #rad-ch2 }
```yaml
# RAD - CH2
type: custom:mushroom-climate-card
entity: climate.rad_ch2
collapsible_controls: false
show_temperature_control: true
fill_container: false
hvac_modes:
  - auto
  - heat_cool
  - cool
  - heat
  - dry
  - fan_only
  - "off"
name: RAD - CH2
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========= FLAME COLOR CONFIG ========= #}
        {% set flame_color = 'deep-orange' %}   {# 'red', 'amber', 'orange', etc. #}
        --flame-color-rgb: var(--rgb-{{ flame_color }});
        {# ===================================== #}

        {# ========== USER CONFIG ========== #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'climate.heatpump' %}
        {% set active_value    = 'heat' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ----------- TRIGGER LOGIC ----------- #}
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
        {# --------- END TRIGGER LOGIC --------- #}

        {% if trigger_active %}
          # --shape-animation: flame-core 1.4s infinite;
          --flame-layer1: flame-layers 1.8s infinite;
          --flame-layer2: ember-pulse 2.4s infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --flame-layer1: none;
          --flame-layer2: none;
          opacity: 0.6;
        {% endif %}

        position: relative;
        transform-origin: 50% 75%;
      }

      /* Flame layers */
      .shape::before,
      .shape::after {
        content: "";
        position: absolute;
        inset: -8px;
        border-radius: inherit;
        pointer-events: none;
        filter: blur(3px);
      }

      .shape::before {
        animation: var(--flame-layer1);
      }

      .shape::after {
        animation: var(--flame-layer2);
      }

      /* Core flame motion: chaotic vertical flicker + heat ripple */
      @keyframes flame-core {
        0%   { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
        12%  { transform: translateY(-2px) scale(1.05);  filter: brightness(1.4) hue-rotate(-10deg); }
        25%  { transform: translateY(1px)  scale(0.98);  filter: brightness(0.9) hue-rotate(8deg); }
        40%  { transform: translateY(-3px) scale(1.07);  filter: brightness(1.5) hue-rotate(-18deg); }
        55%  { transform: translateY(0)    scale(1.02);  filter: brightness(1.2) hue-rotate(10deg); }
        70%  { transform: translateY(-1px) scale(1.04);  filter: brightness(1.35) hue-rotate(-6deg); }
        85%  { transform: translateY(2px)  scale(0.97);  filter: brightness(0.95) hue-rotate(6deg); }
        100% { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
      }

      /* Outer flame shape: shifting blurred glow */
      @keyframes flame-layers {
        0% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
        33% {
          box-shadow:
            0 0 20px 10px rgba(var(--flame-color-rgb), 1),
            0 -16px 30px -8px rgba(255, 160, 0, 0.5);
        }
        66% {
          box-shadow:
            0 0 18px 9px rgba(var(--flame-color-rgb), 0.9),
            0 -8px 20px -6px rgba(255, 220, 0, 0.35);
        }
        100% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
      }

      /* Ember pulse: slow breathing glow */
      @keyframes ember-pulse {
        0% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
        50% {
          box-shadow:
            0 0 50px 18px rgba(var(--flame-color-rgb), 0.5),
            0 0 90px 35px rgba(255, 150, 0, 0.25);
        }
        100% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -17px 0 20px -17px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }
grid_options:
  columns: 6
  rows: 2
```

---

### RAD - CH3 {: #rad-ch3 }
```yaml
# RAD - CH3
type: custom:mushroom-climate-card
entity: climate.rad_ch3
collapsible_controls: false
show_temperature_control: true
fill_container: false
hvac_modes:
  - auto
  - heat_cool
  - cool
  - heat
  - dry
  - fan_only
  - "off"
name: RAD - CH3
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========= FLAME COLOR CONFIG ========= #}
        {% set flame_color = 'deep-orange' %}   {# 'red', 'amber', 'orange', etc. #}
        --flame-color-rgb: var(--rgb-{{ flame_color }});
        {# ===================================== #}

        {# ========== USER CONFIG ========== #}
        {% set use_number      = false %}

        {# STATE MODE SETTINGS #}
        {% set state_entity    = 'climate.heatpump' %}
        {% set active_value    = 'heat' %}

        {# OPTIONAL: NUMBER MODE SETTINGS #}
        {% set number_entity   = 'sensor.plug_power' %}
        {% set number_operator = '>' %}
        {% set threshold       = 0.0 %}
        {# ========== END USER CONFIG ====== #}

        {# ----------- TRIGGER LOGIC ----------- #}
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
        {# --------- END TRIGGER LOGIC --------- #}

        {% if trigger_active %}
          # --shape-animation: flame-core 1.4s infinite;
          --flame-layer1: flame-layers 1.8s infinite;
          --flame-layer2: ember-pulse 2.4s infinite;
          opacity: 1;
        {% else %}
          --shape-animation: none;
          --flame-layer1: none;
          --flame-layer2: none;
          opacity: 0.6;
        {% endif %}

        position: relative;
        transform-origin: 50% 75%;
      }

      /* Flame layers */
      .shape::before,
      .shape::after {
        content: "";
        position: absolute;
        inset: -8px;
        border-radius: inherit;
        pointer-events: none;
        filter: blur(3px);
      }

      .shape::before {
        animation: var(--flame-layer1);
      }

      .shape::after {
        animation: var(--flame-layer2);
      }

      /* Core flame motion: chaotic vertical flicker + heat ripple */
      @keyframes flame-core {
        0%   { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
        12%  { transform: translateY(-2px) scale(1.05);  filter: brightness(1.4) hue-rotate(-10deg); }
        25%  { transform: translateY(1px)  scale(0.98);  filter: brightness(0.9) hue-rotate(8deg); }
        40%  { transform: translateY(-3px) scale(1.07);  filter: brightness(1.5) hue-rotate(-18deg); }
        55%  { transform: translateY(0)    scale(1.02);  filter: brightness(1.2) hue-rotate(10deg); }
        70%  { transform: translateY(-1px) scale(1.04);  filter: brightness(1.35) hue-rotate(-6deg); }
        85%  { transform: translateY(2px)  scale(0.97);  filter: brightness(0.95) hue-rotate(6deg); }
        100% { transform: translateY(0)    scale(1);     filter: brightness(1.1) hue-rotate(0deg); }
      }

      /* Outer flame shape: shifting blurred glow */
      @keyframes flame-layers {
        0% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
        33% {
          box-shadow:
            0 0 20px 10px rgba(var(--flame-color-rgb), 1),
            0 -16px 30px -8px rgba(255, 160, 0, 0.5);
        }
        66% {
          box-shadow:
            0 0 18px 9px rgba(var(--flame-color-rgb), 0.9),
            0 -8px 20px -6px rgba(255, 220, 0, 0.35);
        }
        100% {
          box-shadow:
            0 0 14px 8px rgba(var(--flame-color-rgb), 0.8),
            0 -12px 24px -6px rgba(255, 200, 0, 0.4);
        }
      }

      /* Ember pulse: slow breathing glow */
      @keyframes ember-pulse {
        0% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
        50% {
          box-shadow:
            0 0 50px 18px rgba(var(--flame-color-rgb), 0.5),
            0 0 90px 35px rgba(255, 150, 0, 0.25);
        }
        100% {
          box-shadow:
            0 0 30px 10px rgba(var(--flame-color-rgb), 0.25),
            0 0 60px 20px rgba(255, 120, 0, 0.15);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 65px;
        display: flex;
        margin: -17px 0 20px -17px !important;
        padding-right: 20px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 12px));
      }
grid_options:
  columns: 6
  rows: 2
```
