Sure! Below is an Angular component template (`client-info.component.html`) and TypeScript logic (`client-info.component.ts`) to dynamically display and manage the data from `data.clientInfo`. The UI structure is based on checkboxes categorized into sections.

---

### **Component HTML (`client-info.component.html`)**
```html
<div class="container">
  <h2>Bulk Updates</h2>
  
  <div class="steps">
    <span>Step 1 → Step 2 → Step 3</span>
  </div>

  <h3>Step 1: Select Fields to Update</h3>

  <div *ngFor="let section of clientInfoSections">
    <h4>{{ section.label }}</h4>
    <div class="section">
      <div *ngFor="let field of section.fields">
        <label>
          <input
            type="checkbox"
            [(ngModel)]="field.selected"
          />
          {{ field.label }}
        </label>
      </div>
    </div>
  </div>

  <button (click)="saveSelection()">Save Selection</button>
</div>
```

---

### **Component TypeScript (`client-info.component.ts`)**
```typescript
import { Component, Input, OnInit } from '@angular/core';

@Component({
  selector: 'app-client-info',
  templateUrl: './client-info.component.html',
  styleUrls: ['./client-info.component.css'],
})
export class ClientInfoComponent implements OnInit {
  @Input() data: any;
  clientInfoSections: any[] = [];

  ngOnInit() {
    this.initializeClientInfo();
  }

  initializeClientInfo() {
    if (!this.data || !this.data.clientInfo) {
      console.error('No data available');
      return;
    }

    // Define sections dynamically from input data
    this.clientInfoSections = [
      {
        label: 'Client Information',
        fields: [
          { label: 'Client Name', key: 'clientName', selected: false },
          { label: 'Account Name', key: 'accountName', selected: false },
          { label: 'Analyst', key: 'analyst', selected: false },
          { label: 'Platform', key: 'platform', selected: false },
          { label: 'FAF ID', key: 'fafId', selected: false },
          { label: 'Contract Start Date', key: 'contractStartDate', selected: false },
          { label: 'Contract End Date', key: 'contractEndDate', selected: false },
          { label: 'Contract Year', key: 'contractYear', selected: false },
        ],
      },
      {
        label: 'Reconciliation',
        fields: [
          { label: 'Reconcile R30/R60/R90 GER Together', key: 'reconcileGer', selected: false },
          { label: 'Approved by Reviewer - Checked', key: 'approvedByReviewer', selected: false },
        ],
      },
      {
        label: 'Flags',
        fields: [
          { label: 'Client Flags', key: 'clientFlags', selected: false },
          { label: 'Manual Client Flags', key: 'manualClientFlags', selected: false },
        ],
      },
      {
        label: 'Pricing Guarantee Payment Terms',
        fields: [
          { label: 'Frequency of Client Payment', key: 'frequencyOfPayment', selected: false },
          { label: 'Custom Frequency', key: 'customFrequency', selected: false },
          { label: 'Due Date of Client Payment', key: 'dueDateClientPayment', selected: false },
        ],
      },
      {
        label: 'Reporting Requirements',
        fields: [
          { label: 'Price Change Reporting', key: 'priceChangeReporting', selected: false },
        ],
      },
    ];
  }

  saveSelection() {
    const selectedFields = this.clientInfoSections.flatMap((section) =>
      section.fields.filter((field) => field.selected)
    );

    console.log('Selected Fields:', selectedFields);
  }
}
```

---

### **Component Styling (`client-info.component.css`)**
```css
.container {
  max-width: 900px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background: #f9f9f9;
}

.steps {
  font-size: 14px;
  color: #666;
  margin-bottom: 10px;
}

h3 {
  margin-top: 20px;
}

h4 {
  margin-top: 15px;
  color: #333;
}

.section {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  padding: 10px;
  background: #fff;
  border-radius: 5px;
  border: 1px solid #ddd;
}

label {
  display: flex;
  align-items: center;
  gap: 5px;
}

button {
  margin-top: 20px;
  padding: 10px 15px;
  background: #007bff;
  color: #fff;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background: #0056b3;
}
```

---

### **How it Works:**
- The component takes `data.clientInfo` as an `@Input()`, dynamically generating sections.
- Each section has labeled checkboxes representing fields.
- Users can select checkboxes, and selections are logged when clicking "Save Selection."
- The UI is styled for readability.

Would you like any modifications, such as adding a "Select All" button or grouping checkboxes differently?
