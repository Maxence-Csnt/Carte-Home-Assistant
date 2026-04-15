# Carte Imprimante 🖨️ (COULEURS)



Voici le code à copier dans ton dashboard Home Assistant :

```yaml
#——————————————————
# Crée par Anas Box modifier par Maxence_Csnt
# Carte Imprimante (COULEURS)
# Support : https://discord.gg/s6cZ7Swhh7
#——————————————————
# 📍 Requis (via HACS video d'installation : https://is.gd/CmtqM8) : button-card 📍

type: custom:mushroom-entity-card
entity: sensor.brother_printer
name: Imprimante
icon: mdi:empty
primary_info: name
secondary_info: state
tap_action:
  action: more-info
card_mod:
  style:
    .: |
      ha-card {
        /* ======================== */
        /* USER CONFIG              */
        /* ======================== */
        
        /* 1. Set INK ENTITIES */
        {% set ink_c_ent = 'sensor.printer_c_ink' %}
        {% set ink_m_ent = 'sensor.printer_m_ink' %}
        {% set ink_y_ent = 'sensor.printer_y_ink' %}
        {% set ink_k_ent = 'sensor.printer_k_ink' %}

        {% set states_list = ['printing', 'copying', 'scanning', 'running'] %}
        
        /* 2. Set Shape Size */
        --set-icon-size: 68px;
        
        /* 3. Set Printing Animations 
           Options: 'laser', 'glow', 'icon_glow', 'none' 
        */
        {% set printing_anim = 'icon_glow' %}

        /* 4. Set threshold */
        {% set low_threshold = 15 %}
        
        /* ========================== */

        {% set ink_c = states(ink_c_ent) | int(0) %}
        {% set ink_m = states(ink_m_ent) | int(0) %}
        {% set ink_y = states(ink_y_ent) | int(0) %}
        {% set ink_k = states(ink_k_ent) | int(0) %}
        
        {% set status = states(config.entity) | lower %}
        {% set is_printing = status in states_list %}
        {% set low_ink = (ink_c < low_threshold) or (ink_m < low_threshold) or (ink_y < low_threshold) or (ink_k < low_threshold) %}
        
        /* Determine Status Color & Text */
        {% if is_printing %}
           {% set status_color = '33, 150, 243' %}
           {% set status_text = 'IMPRESSION' %}
           {% set anim_badge = 'none' %}
        {% elif low_ink %}
           {% set status_color = '244, 67, 54' %} 
           {% set status_text = 'NIVEAU D'ENCRE BAS' %}
           {% set anim_badge = 'pulse-alert 2s infinite' %}
        {% else %}
           {% set status_color = '76, 175, 80' %}
           {% set status_text = 'PRÊT' %}
           {% set anim_badge = 'none' %}
        {% endif %}

        /* Logic for Animation Modes */
        {% if is_printing %}
          /* Card Scanner (Whole Card) */
          {% if printing_anim == 'laser' %}
            {% set card_scan_display = 'block' %}
            {% set card_scan_grad = 'linear-gradient(90deg, transparent 20%, rgba(33, 150, 243, 0.2) 45%, rgba(33, 150, 243, 0.9) 50%, rgba(33, 150, 243, 0.2) 55%, transparent 80%)' %}
            {% set icon_scan_anim = 'none' %}
            {% set icon_glass_bg = 'linear-gradient(135deg, rgba(255,255,255,0.15) 0%, transparent 40%, transparent 60%, rgba(255,255,255,0.05) 100%)' %}
            {% set icon_box_shadow = '0 4px 8px rgba(0,0,0,0.3)' %}
          
          {% elif printing_anim == 'glow' %}
            {% set card_scan_display = 'block' %}
            {% set card_scan_grad = 'linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.6), transparent)' %}
            {% set icon_scan_anim = 'none' %}
            {% set icon_glass_bg = 'linear-gradient(135deg, rgba(255,255,255,0.15) 0%, transparent 40%, transparent 60%, rgba(255,255,255,0.05) 100%)' %}
            {% set icon_box_shadow = '0 4px 8px rgba(0,0,0,0.3)' %}

          {% elif printing_anim == 'icon_glow' %}
            /* Icon Only Scanner */
            {% set card_scan_display = 'none' %}
            {% set card_scan_grad = 'none' %}
            /* Dynamic Icon Variables */
            {% set icon_scan_anim = 'icon-sweep 1.5s ease-in-out infinite' %}
            {% set icon_glass_bg = 'linear-gradient(90deg, transparent 0%, rgba(255,255,255,0.1) 40%, rgba(255,255,255,0.9) 50%, rgba(255,255,255,0.1) 60%, transparent 100%)' %}
            {% set icon_box_shadow = '0 0 15px rgba(33, 150, 243, 0.6), inset 0 0 10px rgba(33, 150, 243, 0.2)' %}

          {% else %}
            /* None */
            {% set card_scan_display = 'none' %}
            {% set card_scan_grad = 'none' %}
            {% set icon_scan_anim = 'none' %}
            {% set icon_glass_bg = 'linear-gradient(135deg, rgba(255,255,255,0.15) 0%, transparent 40%, transparent 60%, rgba(255,255,255,0.05) 100%)' %}
            {% set icon_box_shadow = '0 4px 8px rgba(0,0,0,0.3)' %}
          {% endif %}

        {% else %}
          /* Not Printing (Idle) */
          {% set card_scan_display = 'none' %}
          {% set card_scan_grad = 'none' %}
          {% set icon_scan_anim = 'none' %}
          {% set icon_glass_bg = 'linear-gradient(135deg, rgba(255,255,255,0.15) 0%, transparent 40%, transparent 60%, rgba(255,255,255,0.05) 100%)' %}
          {% set icon_box_shadow = '0 4px 8px rgba(0,0,0,0.3)' %}
        {% endif %}

        /* =============================== */
        /* CSS VARIABLES                 */
        /* =============================== */
        
        --level-c: {{ ink_c }}%;
        --level-m: {{ ink_m }}%;
        --level-y: {{ ink_y }}%;
        --level-k: {{ ink_k }}%;
        
        --card-status-color: {{ status_color }};
        --card-badge-anim: {{ anim_badge }};
        --badge-content: "{{ status_text }}";
        
        /* Card Scanner Vars */
        --scanner-display: {{ card_scan_display }};
        --scanner-bg: {{ card_scan_grad }};
        
        /* Icon Scanner Vars */
        --icon-glass-bg: {{ icon_glass_bg }};
        --icon-anim: {{ icon_scan_anim }};
        --icon-shadow: {{ icon_box_shadow }};
        
        transition: all 0.5s ease;
        overflow: hidden; 
        position: relative;
      }

      /* --- STATUS BADGE --- */
      ha-card::before {
        content: var(--badge-content);
        position: absolute;
        top: 10px; right: 10px;
        font-size: 10px;
        font-weight: 900;
        letter-spacing: 0.5px;
        
        color: rgb(var(--card-status-color));
        background: rgba(var(--card-status-color), 0.15);
        border: 1px solid rgba(var(--card-status-color), 0.3);
        
        box-shadow: 0 0 10px rgba(var(--card-status-color), 0.4), inset 0 0 5px rgba(var(--card-status-color), 0.1);
        
        padding: 4px 8px;
        border-radius: 6px;
        z-index: 0; 
        animation: var(--card-badge-anim);
      }

      /* --- CARD SCANNER ANIMATION (Whole Card) --- */
      ha-card::after {
        content: "";
        display: var(--scanner-display);
        position: absolute;
        top: 0; left: 0; bottom: 0;
        width: 30%;
        background: var(--scanner-bg);
        filter: blur(5px);
        z-index: 1; 
        transform: skewX(-10deg) translateX(-200%);
        animation: scanner-sweep 2s ease-in-out infinite;
        pointer-events: none;
      }

      /* --- ANIMATIONS --- */
      @keyframes pulse-alert {
        0% { box-shadow: 0 0 0 0 rgba(var(--card-status-color), 0.7); transform: scale(1); }
        50% { transform: scale(1.05); }
        70% { box-shadow: 0 0 0 10px rgba(var(--card-status-color), 0); }
        100% { box-shadow: 0 0 0 0 rgba(var(--card-status-color), 0); transform: scale(1); }
      }

      @keyframes scanner-sweep {
        0% { left: -50%; opacity: 0; }
        10% { opacity: 1; }
        90% { opacity: 1; }
        100% { left: 150%; opacity: 0; }
      }
    mushroom-shape-icon$: |
      .shape {
        color: transparent !important;
        --icon-size: var(--set-icon-size);
        border-radius: 12px !important; 
        background: #222 !important;     
        border: 1px solid rgba(255,255,255,0.1);
        position: relative;
        overflow: hidden;
        /* Dynamic Shadow/Glow */
        box-shadow: var(--icon-shadow) !important;
        transition: box-shadow 0.3s ease;
      }

      /* The Ink Bars */
      .shape::before {
        content: '';
        position: absolute;
        inset: 2px;
        border-radius: 8px;
        z-index: 2; 
        
        background-image: 
          linear-gradient(to top, #00BCD4 var(--level-c), rgba(0, 188, 212, 0.2) var(--level-c)),
          linear-gradient(to top, #E91E63 var(--level-m), rgba(233, 30, 99, 0.2) var(--level-m)),
          linear-gradient(to top, #FFEB3B var(--level-y), rgba(255, 235, 59, 0.2) var(--level-y)),
          linear-gradient(to top, #9E9E9E var(--level-k), rgba(158, 158, 158, 0.2) var(--level-k));
        
        background-size: 23% 100%;
        background-repeat: no-repeat;
        background-position: 0% 0, 34% 0, 67% 0, 100% 0;
        filter: drop-shadow(0 0 1px rgba(0,0,0,0.5));
      }

      /* Glass Overlay OR Scanner Beam */
      .shape::after {
        content: '';
        position: absolute;
        inset: 0;
        z-index: 3;
        /* Dynamic Background (Glass or Beam) */
        background: var(--icon-glass-bg);
        /* Dynamic Animation */
        animation: var(--icon-anim);
        pointer-events: none;
        background-size: 200% 100%; /* Important for the sweep anim */
      }

      @keyframes icon-sweep {
        0% { background-position: 150% 0; }
        100% { background-position: -50% 0; }
      }

      ha-icon { display: none; }
```
