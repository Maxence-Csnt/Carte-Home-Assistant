# Carte Éclairement ☀️

<img width="516" height="100" alt="Éclairement" src="https://github.com/user-attachments/assets/253cabb7-75cd-4904-98e8-4b1cbfdc4c35" />

Voici le code à copier dans ton dashboard Home Assistant :

```yaml
#——————————————————
# Crée par Anas Box modifier par Maxence_Csnt
# Carte Éclairement
# Support : https://discord.gg/s6cZ7Swhh7
#——————————————————
type: custom:mushroom-entity-card
entity: sensor.detecteur_de_mouvement_illuminance
tap_action:
  action: more-info
icon: mdi:brightness-5
primary_info: state
secondary_info: name
grid_options:
  columns: 12
  rows: 1.25
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set lux = states('sensor.detecteur_de_mouvement_illuminance') | float(0) %}

        {# ------------------------------------------- #}
        {# LIGHT LEVEL → COLOR + EFFECT PRESETS        #}
        {# ------------------------------------------- #}

        {# DEFAULTS (will be overridden by ranges) #}
        {% set rgb = '40,80,255' %}
        {% set anim = 'lux-dark-breathe' %}
        {% set glow_anim = 'lux-dark-glow' %}
        {% set halo_anim = 'lux-dark-halo' %}
        {% set duration = 4.0 %}
        {% set intensity = 0.5 %}

        {# YOUR RANGES / COLORS #####
           < 10      -> deep blue (very dark)
           10 - <50  -> purple (dim)
           50 - <200 -> soft yellow (normal)
           200 - <500 -> warm orange (bright)
           >= 500    -> near white (very bright)
        ########################## #}

        {# RANGES / COLORS #}
        {# You can change aqi number below if needed #}

        {% if lux < 10 %}
          {# DEEP BLUE - VERY DARK #}
          {% set rgb = '40,80,255' %}
          {% set anim = 'lux-dark-breathe' %}
          {% set glow_anim = 'lux-dark-glow' %}
          {% set halo_anim = 'lux-dark-halo' %}
          {% set duration = 4.4 %}
          {% set intensity = 0.4 %}

        {% elif lux < 50 %}
          {# PURPLE - DIM #}
          {% set rgb = '140,80,220' %}
          {% set anim = 'lux-dim-wave' %}
          {% set glow_anim = 'lux-dim-glow' %}
          {% set halo_anim = 'lux-dim-halo' %}
          {% set duration = 3.6 %}
          {% set intensity = 0.55 %}

        {% elif lux < 200 %}
          {# SOFT YELLOW - COMFY #}
          {% set rgb = '255,210,80' %}
          {% set anim = 'lux-comfy-breathe' %}
          {% set glow_anim = 'lux-comfy-glow' %}
          {% set halo_anim = 'lux-comfy-halo' %}
          {% set duration = 3.0 %}
          {% set intensity = 0.6 %}

        {% elif lux < 500 %}
          {# WARM ORANGE - BRIGHT #}
          {% set rgb = '255,160,60' %}
          {% set anim = 'lux-bright-pulse' %}
          {% set glow_anim = 'lux-bright-glow' %}
          {% set halo_anim = 'lux-bright-halo' %}
          {% set duration = 2.6 %}
          {% set intensity = 0.8 %}

        {% else %}
          {# NEAR WHITE - VERY BRIGHT #}
          {% set rgb = '255,250,230' %}
          {% set anim = 'lux-sun-shimmer' %}
          {% set glow_anim = 'lux-sun-glow' %}
          {% set halo_anim = 'lux-sun-halo' %}
          {% set duration = 2.0 %}
          {% set intensity = 1.0 %}
        {% endif %}

        {# Apply variables #}
        --lux-rgb: {{ rgb }};
        --lux-intensity: {{ intensity }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --lux-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --lux-halo-animation: {{ halo_anim }} {{ (duration * 1.15) | round(2) }}s ease-in-out infinite;

        opacity: 1;

        /* Icon color follows the light level */
        --icon-color: rgba({{ rgb }}, 1);

        /* Neutral base for the shape */
        background-color: rgba(77, 77, 77, 0.1) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255, 255, 255, 0.06);

        position: relative;
        transform-origin: 50% 60%;
        animation: var(--shape-animation);
      }

      /* Glow layers */
      .shape::before,
      .shape::after {
        content: '';
        position: absolute;
        border-radius: inherit;
        pointer-events: none;
      }

      .shape::before {
        inset: -8px;
        animation: var(--lux-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--lux-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== DARK ========== */
      @keyframes lux-dark-breathe {
        0%   { transform: scale(0.96); }
        50%  { transform: scale(1.03); }
        100% { transform: scale(0.96); }
      }

      @keyframes lux-dark-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--lux-rgb), 0.6),
            0 0 34px 6 rgba(var(--lux-rgb), 0.55);
        }
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--lux-rgb), 0.95),
            0 0 50px 10px rgba(var(--lux-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--lux-rgb), 0.6),
            0 0 34px 6 rgba(var(--lux-rgb), 0.55);
        }
      }

      @keyframes lux-dark-halo {
        0% {
          box-shadow:
            0 0 80px 20px rgba(var(--lux-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
        50% {
          box-shadow:
            0 0 130px 36px rgba(var(--lux-rgb), 0.5),
            0 -34px 100px -8px rgba(240, 250, 255, 0.8);
        }
        100% {
          box-shadow:
            0 0 80px 20px rgba(var(--lux-rgb), 0.35),
            0 -20px 80px -14px rgba(220, 240, 255, 0.55);
        }
      }

      /* ========== DIM ========== */
      @keyframes lux-dim-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes lux-dim-glow {
        0% {
          box-shadow:
            0 0 22px 0 rgba(var(--lux-rgb), 0.6),
            0 0 34px 4 rgba(var(--lux-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 28px 2 rgba(var(--lux-rgb), 0.95),
            0 0 48px 12px rgba(var(--lux-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 22px 0 rgba(var(--lux-rgb), 0.6),
            0 0 34px 4 rgba(var(--lux-rgb), 0.7);
        }
      }

      @keyframes lux-dim-halo {
        0% {
          box-shadow:
            0 0 90px 26px rgba(var(--lux-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
        50% {
          box-shadow:
            0 0 140px 42px rgba(var(--lux-rgb), 0.45),
            0 30px 110px -10px rgba(0, 255, 255, 0.5);
        }
        100% {
          box-shadow:
            0 0 90px 26px rgba(var(--lux-rgb), 0.35),
            0 18px 80px -12px rgba(0, 220, 255, 0.35);
        }
      }

      /* ========== COMFY ========== */
      @keyframes lux-comfy-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.05); }
        100% { transform: scale(0.98); }
      }

      @keyframes lux-comfy-glow {
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--lux-rgb), 0.9),
            0 0 42px 10px rgba(var(--lux-rgb), 0.85);
        }
      }

      @keyframes lux-comfy-halo {
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--lux-rgb), 0.45),
            0 26px 80px -10px rgba(180, 255, 200, 0.5);
        }
      }

      /* ========== BRIGHT ========== */
      @keyframes lux-bright-pulse {
        0%   { transform: scale(1); }
        50%  { transform: scale(1.07); }
        100% { transform: scale(1); }
      }

      @keyframes lux-bright-glow {
        50% {
          box-shadow:
            0 0 30px 4 rgba(var(--lux-rgb), 0.95),
            0 0 54px 14px rgba(var(--lux-rgb), 0.9);
        }
      }

      @keyframes lux-bright-halo {
        50% {
          box-shadow:
            0 0 140px 48px rgba(var(--lux-rgb), 0.55),
            0 26px 100px -10px rgba(255, 210, 150, 0.5);
        }
      }

      /* ========== VERY BRIGHT / SUN ========== */
      @keyframes lux-sun-shimmer {
        0%   { transform: scale(1); filter: blur(0); }
        50%  { transform: scale(1.08); filter: blur(0.6px); }
        100% { transform: scale(1); filter: blur(0); }
      }

      @keyframes lux-sun-glow {
        50% {
          box-shadow:
            0 0 34px 6 rgba(var(--lux-rgb), 1),
            0 0 62px 14px rgba(var(--lux-rgb), 0.95);
        }
      }

      @keyframes lux-sun-halo {
        50% {
          box-shadow:
            0 0 160px 60px rgba(var(--lux-rgb), 0.6),
            0 34px 120px -12px rgba(255, 230, 180, 0.6);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        display: flex;
        margin: -18px 0 10px -20px !important;
        padding-right: 22px;
        padding-bottom: 10px;
      }
      ha-card {
        clip-path: inset(0 0 0 0 round var(--ha-card-border-radius, 14px));
        
        /* FONT SIZE & SPACING SETTINGS */
        --card-primary-font-size: 1.5rem !important;
        
        /* Increases vertical space between primary and secondary */
        --card-primary-line-height: 1.3 !important;
      }
```
