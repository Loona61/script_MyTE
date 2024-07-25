// Fonction pour sélectionner l'option d'un select par valeur
function selectOptionByValue(selectElement, value) {
    for (let option of selectElement.options) {
        if (option.value === value) {
            selectElement.value = value;
            selectElement.dispatchEvent(new Event('change', { bubbles: true }));
            break;
        }
    }
}

// Fonction pour vérifier et ouvrir la popup si nécessaire
function ensurePopupIsOpen(callback) {
    if (document.querySelector('myte-punch-clock-popup')) {
        callback();
    } else {
        document.querySelector('#working-hours-side-header').click();
        setTimeout(function() {
            if (document.querySelector('myte-punch-clock-popup')) {
                callback();
            } else {
                console.error("La popup n'a pas pu être ouverte.");
            }
        }, 2000); // Attendre 2 secondes pour que la popup se charge
    }
}

// Fonction pour récupérer les dates des colonnes
function getColumnDates() {
    const dateColumns = {};
    document.querySelectorAll('.ag-header-cell[col-id^="Date"]').forEach((headerCell) => {
        const colId = headerCell.getAttribute('col-id');
        const dateSpan = headerCell.querySelector('.header-date-cell span:nth-child(2)');
        if (dateSpan) {
            const dateText = dateSpan.textContent.trim();
            dateColumns[colId] = dateText;
        }
    });
    return dateColumns;
}

// Fonction pour récupérer le work schedule
function getWorkSchedule(rowDiv, colId) {
    if (!rowDiv) {
        return null;
    }
    let workScheduleDiv = rowDiv.querySelector(`div[col-id="${colId}"] .hours-container span[aria-hidden="true"]`);
    if (workScheduleDiv) {
        return workScheduleDiv.textContent.trim();
    } else {
        return null;
    }
}

// Fonction pour remplir les champs en fonction du work schedule
function fillFieldsByWorkSchedule(workSchedule, hoursSelect, minutesSelect, meridianSelect, breakSelect) {
    // Normaliser la valeur de workSchedule en remplaçant la virgule par un point
    const normalizedWorkSchedule = workSchedule.replace(',', '.');
        
    switch (normalizedWorkSchedule) {
        case '7.5':
            selectOptionByValue(hoursSelect, '5');
            selectOptionByValue(minutesSelect, '30');
            selectOptionByValue(meridianSelect, 'pm');
            selectOptionByValue(breakSelect, '1');
            break;
        case '7.0':
            selectOptionByValue(hoursSelect, '5');
            selectOptionByValue(minutesSelect, '0');
            selectOptionByValue(meridianSelect, 'pm');
            selectOptionByValue(breakSelect, '1');
            break;
        case '8.5':
            selectOptionByValue(hoursSelect, '7');
            selectOptionByValue(minutesSelect, '30');
            selectOptionByValue(meridianSelect, 'pm');
            selectOptionByValue(breakSelect, '1');
            break;
        case '3.0':
            selectOptionByValue(hoursSelect, '12');
            selectOptionByValue(minutesSelect, '0');
            selectOptionByValue(meridianSelect, 'am');
            selectOptionByValue(breakSelect, '0');
            break;
        default:
            console.error("Work schedule non reconnu : " + workSchedule);
            break;
    }
}

// Fonction principale pour remplir les champs
function fillFields() {
    const dateColumns = getColumnDates();

    // Récupérer les work schedules depuis le tableau principal
    const workSchedules = {};
    document.querySelectorAll('div[role="row"]').forEach(function(rowDiv, rowIndex) {
        for (let colId in dateColumns) {
            let workSchedule = getWorkSchedule(rowDiv, colId);
            if (workSchedule) {
                workSchedules[dateColumns[colId]] = workSchedule;
            }
        }
    });

    // Remplir les champs dans la popup
    document.querySelectorAll('myte-punch-clock-popup div[role="row"]').forEach(function(rowDiv) {
        if (rowDiv.querySelector('.special-cell')) {
            console.log("Jour férié ou week-end détecté, saut de cette ligne.");
            return; // Ignorer les jours fériés et les week-ends
        }

        let dateDiv = rowDiv.querySelector('div[col-id="dateTime"] .spanned-cell');
        if (dateDiv) {
            let dateText = dateDiv.textContent.trim();
            let numericDate = dateText.split('/')[1].trim(); // Extraire la partie après le '/'
            numericDate = numericDate.padStart(2, '0'); // Ajouter un zéro devant si nécessaire
            if (workSchedules[numericDate]) {
                let workSchedule = workSchedules[numericDate];

                // Remplir les champs workStartTime
                let startTimeDiv = rowDiv.querySelector('div[col-id="workStartTime"]');
                if (startTimeDiv) {
                    let hoursSelect = startTimeDiv.querySelector('select[name="hours"]');
                    let minutesSelect = startTimeDiv.querySelector('select[name="minutes"]');
                    let meridianSelect = startTimeDiv.querySelector('select[name="meridian"]');
                    if (hoursSelect && minutesSelect && meridianSelect) {
                        selectOptionByValue(hoursSelect, '9');
                        selectOptionByValue(minutesSelect, '0');
                        selectOptionByValue(meridianSelect, 'am');
                    }
                }

                // Remplir les champs workEndTime et breakDuration
                let endTimeDiv = rowDiv.querySelector('div[col-id="workEndTime"]');
                if (endTimeDiv) {
                    let hoursSelect = endTimeDiv.querySelector('select[name="hours"]');
                    let minutesSelect = endTimeDiv.querySelector('select[name="minutes"]');
                    let meridianSelect = endTimeDiv.querySelector('select[name="meridian"]');
                    let breakDiv = rowDiv.querySelector('div[col-id="breakDuration"]');
                    if (hoursSelect && minutesSelect && meridianSelect && breakDiv) {
                        fillFieldsByWorkSchedule(workSchedule, hoursSelect, minutesSelect, meridianSelect, breakDiv.querySelector('select[name="breakDuration"]'));
                    }
                }
            } else {
                console.warn("Work schedule non trouvé pour la date : " + dateText);
            }
        }
    });

    console.log("Champs remplis avec succès !");
}

// Vérifier et ouvrir la popup si nécessaire, puis remplir les champs
ensurePopupIsOpen(fillFields);
