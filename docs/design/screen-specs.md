# SaveIt Screen Specifications

## Hôm nay

**Purpose:** create a Check-in with one tap.

**Content:** title, random header mascot, scrollable stable Action grid, transient Check-in snackbar, and floating navigation. The first release seeds 16 Built-in Actions: Thức dậy, Uống nước, Uống thuốc, Ăn sáng, Đi làm, Ăn trưa, Hít thở sâu, Vệ sinh nhẹ, Vệ sinh, Tập thể dục, Về nhà, Ăn tối, Tắm, Đánh răng, Thư giãn, Đi ngủ.

**States:** populated; snackbar visible; reorder mode; all Actions archived. The all-archived state retains the title/mascot and says `Chưa có hành động trên Hôm nay` with one `Thêm hành động` action.

## Add/Edit Action

**Purpose:** create or change an Action without adding planning complexity.

**Fields:** name, icon picker, color picker. Save is disabled until all fields are valid. Names are trimmed; duplicate names are allowed because Actions retain distinct identities. Editing a Built-in Action uses the same form and rules as a Personal Action.

**States:** create, edit, validation error, unsaved-change confirmation.

## Reorder Actions

**Purpose:** make Home position intentional and stable.

**Content:** one ordered list with icon, name, and drag handle; Save and Cancel. Dragging is keyboard and screen-reader operable through Move up/Move down actions.

## Lịch sử

**Purpose:** review and correct recorded facts.

**Content:** screen title; one compact filter-aware count; Action filter; date jump; reverse-chronological sections; Check-in rows with Action, time, and Reminder-origin indicator when applicable; floating navigation.

**States:** populated, no results for filter/date, no Check-ins, edit result, deleted result.

## Edit Check-in

**Purpose:** correct an Action or timestamp.

**Fields:** Action selector, date, time. Actions referenced only by old history remain selectable for an existing Check-in. Destructive Delete is separated from Save and requires confirmation.

## Nhắc nhở

**Purpose:** understand what will notify next and manage schedules.

**Content:** title; permission warning when notifications are unavailable; rows ordered by time with Action, `HH:mm`, weekday summary, toggle, and next-fire context; floating navigation.

**States:** populated, no Reminders, notifications denied, all disabled, identical Reminder rows.

## Add/Edit Reminder

**Purpose:** explicitly schedule one Action notification.

**Fields:** Action, time, seven weekday toggles, enabled state. From a Check-in, Action/time are prefilled and all weekdays selected. Save persists even if notification permission is denied. Delete exists only in edit mode.

## Settings / About

**Purpose:** control haptics and identify the installed build.

**Content:** Haptics switch; app name SaveIt; semantic version; build number; links required by platform distribution only when later supplied. No other preferences.

## System surfaces

**Notification:** Action name, scheduled time context, and `Đã làm` action. Copy remains neutral, especially for medicine: `Nhắc bạn: Uống thuốc`, never dosage or medical direction.

**Permission prompt:** invoked only as part of first Reminder save, preceded by a short in-app explanation of why notifications are needed.

**Destructive confirmation:** names the affected object and consequence. Archiving an Action states that Check-ins remain and Reminders will be removed.
