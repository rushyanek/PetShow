# PetShow

Плагин для Minecraft серверов (Spigot/Paper 1.16.5 - 1.21+), добавляющий систему летающих питомцев-голов с настраиваемыми эффектами и атрибутами.

## ✨ Возможности

- **Летающие питомцы**: Головы, которые следуют за игроком по орбите
- **Кастомные текстуры**: Поддержка base64 текстур для голов
- **Эффекты и атрибуты**: Настраиваемые зелья и бонусы к характеристикам
- **Система передачи**: Питомцы могут переходить к убийце при смерти владельца
- **GUI меню**: Удобный интерфейс для выбора питомцев
- **Персистентность**: Сохранение питомцев в базе данных
- **Права доступа**: Гибкая система разрешений

## 🚀 Установка

1. Скачайте последний релиз из [Releases](../../releases)
2. Поместите `PetShow.jar` в папку `plugins/` вашего сервера
3. Перезапустите сервер
4. Настройте конфигурацию в `plugins/PetShow/config.yml`

## 📋 Требования

- **Minecraft**: 1.16.5 - 1.21+
- **Сервер**: Spigot, Paper или совместимые форки
- **Java**: 8 или выше

## ⚙️ Конфигурация

### Основные настройки (`config.yml`)

```yaml
# Сообщения плагина
messages:
  no_permission: "&cУ вас нет прав для использования этой команды!"
  pet_given: "&aПитомец &e%pet% &aвыдан игроку &e%player%"
  pet_reset: "&cПитомец игрока &e%player% &cснят"
  pet_not_exist: "&cТакого питомца не существует!"
  player_not_found: "&cИгрок не найден!"

# Политика передачи питомцев при смерти
# player - питомец остается у жертвы
# killer - питомец передается убийце
# auto - зависит от настройки drop_to_kill у питомца
pet_add: "auto"

# Определения питомцев
pets:
  Demon_pet:
    name: "&c&lДемон"
    basehead: "eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvMjRiYmNiYWVhYzJjNzBkZWRlOGZhZDU2ODMxMjAxN2M0MDM0OTNlYWJjNGI0YTFhYmZiYjhjN2I2MTU3ODc4NCJ9fX0="
    offset-x: 1.5
    offset-y: 1.6
    offset-z: 0.0
    speed: 0.25
    head-rotation: 0.0
    drop_to_kill: true
    drop_kill_command: "say %victim% был убит %killer%!"
    effects:
      - "STRENGTH:3:999999"
      - "RESISTANCE:2:999999"
      - "REGENERATION:1:999999"
    attributes:
      - "GENERIC_MAX_HEALTH:10.0"
      - "GENERIC_ARMOR:4.0"
```

### GUI меню (`gui.yml`)

```yaml
menu_title: "&8>>> &8Стражи"
size: 27

items:
  Demon:
    material: "basehead-eyJ0ZXh0dXJlcyI6eyJTS0lOIjp7InVybCI6Imh0dHA6Ly90ZXh0dXJlcy5taW5lY3JhZnQubmV0L3RleHR1cmUvMjRiYmNiYWVhYzJjNzBkZWRlOGZhZDU2ODMxMjAxN2M0MDM0OTNlYWJjNGI0YTFhYmZiYjhjN2I2MTU3ODc4NCJ9fX0="
    slot: 13
    priority: 1
    view_requirement:
      requirements:
        complete:
          type: "has permission"
          permission: "straj.demon"
    left_click_commands:
      - "[console] pet set %player_name% Demon_pet"
      - "[close]"
      - "[refresh]"
    right_click_commands:
      - "[console] pet reset %player_name%"
      - "[message] &7[&6&lOneTime&7]&f С вас снят Страж"
      - "[close]"
      - "[refresh]"
    display_name: "&x&F&F&0&0&0&0С&x&F&5&0&1&0&1т&x&E&C&0&2&0&2р&x&E&2&0&3&0&3а&x&D&8&0&3&0&3ж &x&C&5&0&5&0&5» &x&B&1&0&7&0&7Д&x&A&8&0&8&0&8е&x&9&E&0&8&0&8м&x&9&4&0&9&0&9о&x&8&B&0&A&0&Aн&x&8&1&0&B&0&Bа"
    lore:
      - ""
      - "&4&l↗ &fВыдаёт эффекты:"
      - ""
      - " &7Сила &fIII &9(∞)"
      - " &7Сопротивление &fII &9(∞)"
      - " &7Регенерация &fI &9(∞)"
      - ""
      - "&4&l↗ &fВыдаёт атрибуты:"
      - ""
      - " &7+ &c❤❤❤❤❤"
      - " &7+ &e 2.0 к броне"
      - ""
      - "&4&l↗ &fОсобенности:"
      - ""
      - " &cДанный страж в случаи вашей смерти от другого игрока"
      - " &cперейдёт к вашему убийце"
      - ""
      - "&4&l➥ &7Нажмите ЛКМ, чтобы надеть"
      - "&4&l➥ &7Нажмите ПКМ, чтобы снять"
```

# 🎮 Команды

| Команда | Описание | Права |
|---------|----------|-------|
| `/pet` | Открыть меню питомцев | `petshow.menu` |
| `/pet set <игрок> <питомец>` | Выдать питомца игроку | `petshow.admin` |
| `/pet reset <игрок>` | Снять питомца с игрока | `petshow.admin` |
| `/pet reload` | Перезагрузить конфигурацию | `petshow.admin` |


# GUI команды
- `[console] <команда>` - Выполнить от имени консоли
- `[player] <команда>` - Выполнить от имени игрока
- `[message] <текст>` - Отправить сообщение
- `[sound] <звук>` - Воспроизвести звук
- `[effect] <эффект>` - Показать визуальный эффект
- `[close]` - Закрыть меню
- `[refresh]` - Обновить меню


---

**PetShow** - делаем ваш сервер более интересным! 🎮✨
