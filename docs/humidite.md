# Carte Humidité 💦

Voici le code à copier dans ton dashboard Home Assistant :

```yaml
#——————————————————
# Crée par Anas Box modifier par Maxence_Csnt
# Carte Humidité
# Support : https://discord.gg/s6cZ7Swhh7
#——————————————————
# 📍 Requis (via HACS video d'installation : https://is.gd/CmtqM8) : vertical stack In Card, Mushroom, Mushroom Themes et card-mod 📍

type: custom:mushroom-entity-card
entity: sensor.livingroom_humidity
tap_action:
  action: more-info
icon: mdi:water-percent
name: Living room humidity
primary_info: state
secondary_info: name
card_mod:
  style:
    mushroom-shape-icon$: |
      .shape {
        {# ========== CONFIG ========== #}
        {% set hum = states('sensor.livingroom_humidity') | float(0) %}

        {# DEFAULTS #}
        {% set rgb = '120,210,255' %}
        {% set anim = 'hum-good-breathe' %}
        {% set glow_anim = 'hum-good-glow' %}
        {% set halo_anim = 'hum-good-halo' %}
        {% set duration = 3.2 %}

        {# RANGES / COLORS #}
        {# You can change number below if needed #}

        {% if hum < 40 %}
          {# BAD - dry - dark blue #}
          {% set rgb = '0,80,200' %}
          {% set anim = 'hum-bad-pulse' %}
          {% set glow_anim = 'hum-bad-glow' %}
          {% set halo_anim = 'hum-bad-halo' %}
          {% set duration = 2.8 %}
        {% elif hum <= 60 %}
          {# GOOD - light blue #}
          {% set rgb = '120,210,255' %}
          {% set anim = 'hum-good-breathe' %}
          {% set glow_anim = 'hum-good-glow' %}
          {% set halo_anim = 'hum-good-halo' %}
          {% set duration = 3.4 %}
        {% else %}
          {# MIDDLE / humid - medium blue #}
          {% set rgb = '40,140,255' %}
          {% set anim = 'hum-mid-wave' %}
          {% set glow_anim = 'hum-mid-glow' %}
          {% set halo_anim = 'hum-mid-halo' %}
          {% set duration = 3.0 %}
        {% endif %}

        --hum-rgb: {{ rgb }};
        --shape-animation: {{ anim }} {{ duration }}s ease-in-out infinite;
        --hum-glow-animation: {{ glow_anim }} {{ (duration * 0.9) | round(2) }}s ease-in-out infinite;
        --hum-halo-animation: {{ halo_anim }} {{ (duration * 1.1) | round(2) }}s ease-in-out infinite;

        /* Icon color follows humidity color */
        --icon-color: rgba({{ rgb }}, 1);

        /* Neutral pill so theme blue does not leak through */
        background-color: rgba(77,77,77,0.2) !important;
        box-shadow: none !important;
        border: 1px solid rgba(255,255,255,0.06);

        opacity: 1;
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
        animation: var(--hum-glow-animation);
      }

      .shape::after {
        inset: -22px;
        animation: var(--hum-halo-animation);
        mix-blend-mode: screen;
      }

      /* ========== GOOD - light blue ========== */
      @keyframes hum-good-breathe {
        0%   { transform: scale(0.98); }
        50%  { transform: scale(1.04); }
        100% { transform: scale(0.98); }
      }

      @keyframes hum-good-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--hum-rgb), 0.55),
            0 0 30px 4 rgba(var(--hum-rgb), 0.6);
        }
        50% {
          box-shadow:
            0 0 24px 4 rgba(var(--hum-rgb), 0.9),
            0 0 44px 10px rgba(var(--hum-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--hum-rgb), 0.55),
            0 0 30px 4 rgba(var(--hum-rgb), 0.6);
        }
      }

      @keyframes hum-good-halo {
        0% {
          box-shadow:
            0 0 80px 24px rgba(var(--hum-rgb), 0.35),
            0 18px 70px -12px rgba(180,230,255,0.3);
        }
        50% {
          box-shadow:
            0 0 120px 40px rgba(var(--hum-rgb), 0.45),
            0 26px 90px -10px rgba(200,240,255,0.45);
        }
        100% {
          box-shadow:
            0 0 80px 24px rgba(var(--hum-rgb), 0.35),
            0 18px 70px -12px rgba(180,230,255,0.3);
        }
      }

      /* ========== MIDDLE / humid - medium blue ========== */
      @keyframes hum-mid-wave {
        0%   { transform: translateX(0); }
        25%  { transform: translateX(-1px); }
        50%  { transform: translateX(1px) translateY(-1px); }
        75%  { transform: translateX(-1px); }
        100% { transform: translateX(0); }
      }

      @keyframes hum-mid-glow {
        0% {
          box-shadow:
            0 0 20px 0 rgba(var(--hum-rgb), 0.6),
            0 0 32px 4 rgba(var(--hum-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 28px 3 rgba(var(--hum-rgb), 0.95),
            0 0 48px 10px rgba(var(--hum-rgb), 0.85);
        }
        100% {
          box-shadow:
            0 0 20px 0 rgba(var(--hum-rgb), 0.6),
            0 0 32px 4 rgba(var(--hum-rgb), 0.7);
        }
      }

      @keyframes hum-mid-halo {
        0% {
          box-shadow:
            0 0 90px 26px rgba(var(--hum-rgb), 0.4),
            0 18px 80px -12px rgba(80,190,255,0.35);
        }
        50% {
          box-shadow:
            0 0 135px 42px rgba(var(--hum-rgb), 0.5),
            0 28px 105px -10px rgba(100,210,255,0.5);
        }
        100% {
          box-shadow:
            0 0 90px 26px rgba(var(--hum-rgb), 0.4),
            0 18px 80px -12px rgba(80,190,255,0.35);
        }
      }

      /* ========== BAD - dry - dark blue ========== */
      @keyframes hum-bad-pulse {
        0%   { transform: scale(0.97); }
        40%  { transform: scale(1.03); }
        100% { transform: scale(0.97); }
      }

      @keyframes hum-bad-glow {
        0% {
          box-shadow:
            0 0 18px 0 rgba(var(--hum-rgb), 0.6),
            0 0 28px 4 rgba(var(--hum-rgb), 0.7);
        }
        50% {
          box-shadow:
            0 0 26px 4 rgba(var(--hum-rgb), 0.95),
            0 0 44px 12px rgba(var(--hum-rgb), 0.9);
        }
        100% {
          box-shadow:
            0 0 18px 0 rgba(var(--hum-rgb), 0.6),
            0 0 28px 4 rgba(var(--hum-rgb), 0.7);
        }
      }

      @keyframes hum-bad-halo {
        0% {
          box-shadow:
            0 0 80px 22px rgba(var(--hum-rgb), 0.45),
            0 18px 75px -10px rgba(0,70,160,0.5);
        }
        50% {
          box-shadow:
            0 0 130px 40px rgba(var(--hum-rgb), 0.6),
            0 26px 100px -8px rgba(0,90,190,0.65);
        }
        100% {
          box-shadow:
            0 0 80px 22px rgba(var(--hum-rgb), 0.45),
            0 18px 75px -10px rgba(0,70,160,0.5);
        }
      }
    .: |
      mushroom-shape-icon {
        --icon-size: 64px;
        --icon-color: rgba(var(--hum-rgb),1) !important;
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
grid_options:
  columns: 12
  rows: 1.5
```
