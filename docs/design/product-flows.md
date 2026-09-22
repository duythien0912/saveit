# SaveIt Product Flows

These flows describe externally visible behavior. Domain terms use `CONTEXT.md`.

## App start

1. Launch opens Hôm nay directly; there is no onboarding or account gate.
2. On first launch, seed the 16 Built-in Actions in their canonical order.
3. Restore archived state, manual order, Personal Actions, Check-ins, Reminders, and haptics preference from local storage.
4. Choose a header mascot frame once for this Home activation.
5. Notification permission is not requested until the person first saves a Reminder.

## Create and undo a Check-in

1. The person taps an Action tile.
2. SaveIt creates one Check-in at the device's current local time and emits light haptic feedback when enabled.
3. A snackbar shows the new Check-in, a random mascot pose, Reminder affordance, and Undo.
4. Undo deletes that exact Check-in and restores the preceding UI state.
5. Repeated intentional taps create repeated Check-ins. One physical tap must never create more than one.

## Create a Reminder from a Check-in

1. After every Check-in, the snackbar offers `Nhắc tôi giờ này`, even when similar or identical Reminders already exist.
2. Selecting it opens Reminder editor with the Action and Check-in time prefilled; repeat defaults to every day.
3. The person may change time and select individual weekdays.
4. Saving the first Reminder triggers the native notification permission request.
5. If permission is granted, SaveIt persists and schedules the Reminder.
6. If permission is denied, SaveIt still persists the Reminder as `Chưa được phép thông báo` and provides a Settings link from the Reminder screen.
7. Identical Reminders are allowed deliberately. SaveIt does not merge, warn about, or suppress them.

## Notification and Reminder Check-in

1. At schedule time, the system notification names the Action and provides `Đã làm`.
2. Receiving, viewing, or dismissing the notification does not create a Check-in.
3. Selecting `Đã làm` creates a Reminder Check-in using the actual selection time, not the scheduled time.
4. Opening the notification without selecting `Đã làm` navigates to SaveIt without recording completion.
5. If the app cannot process the action immediately, it queues the intent idempotently and records once when storage becomes available.

## Create a Personal Action

1. The person selects the separate plus Action from any destination.
2. A sheet opens with required name, icon, and color.
3. Save validates a nonblank name and selected icon/color, creates the Personal Action, appends it to the Home grid, and closes back to the previous destination.
4. Cancel discards changes.

## Edit, reorder, and archive an Action

1. Long press an Action tile to open Edit, Reorder, and Archive.
2. Edit may change name, icon, and color for Built-in or Personal Actions; existing Check-ins display the updated Action identity.
3. Reorder enters a dedicated reorder state with drag handles; Save persists the explicit order.
4. Archive requires confirmation. It removes the Action from Home, keeps its Check-ins in History, and removes all of its Reminders from future scheduling.
5. Archived Actions remain resolvable in historical records.

## Browse and correct History

1. Lịch sử opens a reverse-chronological timeline grouped by local calendar day.
2. A single summary line reflects the current Action filter, for example `Uống nước · 6 lần hôm nay`; with no filter it reports all Check-ins.
3. The person can filter by Action and jump to a date using a calendar control.
4. Selecting a Check-in opens Edit Check-in.
5. Edit may change time or assign another active or archived Action. Save updates the timeline and summary.
6. Delete requires confirmation and removes only that Check-in; it does not modify Reminders.

## Manage Reminders

1. Nhắc nhở lists enabled and disabled Reminders ordered by next time of day across Actions.
2. Each row shows Action, time, selected weekdays, enabled state, and permission warning when required.
3. Toggle changes scheduling without deleting the Reminder.
4. Selecting a row opens Reminder editor for Action, time, weekdays, and enabled state.
5. Delete requires confirmation and cancels only that Reminder.
6. Multiple and identical Reminders remain separate rows.

## Settings

1. Settings is reached from a small overflow affordance on non-Home management screens, not from the Home header.
2. The only preference is Haptics on/off.
3. About shows app name, semantic version, and build number.
4. There is no account, sync, analytics, theme, export, backup, or bulk-delete UI in the first release.

## Date, time, and lifecycle rules

- Store instants in UTC and retain the device timezone used for presentation-sensitive scheduling.
- History groups by the current local timezone.
- Reminder weekday/time schedules follow the device's local timezone after timezone changes.
- Daylight-saving transitions use platform scheduling behavior and never create a Check-in automatically.
- App reinstall or OS data deletion removes local data; SaveIt makes no cloud recovery claim.
