To display custom icons like the ones in your screenshot (e.g., a filled circle for the current step, a checkmark for a completed step), you can use the `MatStepperIcon` directive provided by Angular Material. Here's how to do it:

---

### 1. Customize Step Icons
Modify the stepper to include custom icons for active, completed, and future steps:

#### Updated HTML Template
```html
<mat-horizontal-stepper linear #stepper>
  <!-- Step 1 -->
  <mat-step [completed]="step1Completed" label="Step 1">
    <ng-template matStepLabel>
      <div>
        <mat-icon *ngIf="stepper.selectedIndex > 0; else step1Active">done</mat-icon>
        <ng-template #step1Active>
          <span *ngIf="stepper.selectedIndex === 0" class="active-icon"></span>
        </ng-template>
        Step 1
      </div>
    </ng-template>
    <div>
      <h3>Step 1: Select Fields to Update</h3>
      <button mat-button matStepperNext (click)="completeStep1()">Next</button>
    </div>
  </mat-step>

  <!-- Step 2 -->
  <mat-step [completed]="step2Completed">
    <div>
      <h3>Step 2</h3>
  </mat-step>
</mat-horizontal-stepper>```

To implement custom icons in your Angular Material stepper, you'll need to use a combination of Angular Material's `MatStepperIcon` directive and some custom CSS for styling. Below is a detailed example:

---

### Updated Implementation for Custom Icons

#### 1. Customize Icons Using `MatStepperIcon`
You can replace the default icons with custom ones like a checkmark for completed steps or a circle for the current step.

#### Updated HTML Template:
```html
<mat-horizontal-stepper linear #stepper>
  <!-- Step 1 -->
  <mat-step [completed]="step1Completed">
    <ng-template matStepLabel>
      <div class="step-label">
        <mat-icon *ngIf="step1Completed">check_circle</mat-icon>
        <span *ngIf="!step1Completed && stepper.selectedIndex === 0" class="active-icon"></span>
        <span *ngIf="!step1Completed && stepper.selectedIndex !== 0" class="inactive-icon"></span>
        Step 1
      </div>
    </ng-template>
    <div>
      <h3>Step 1: Select Fields to Update</h3>
      <button mat-button matStepperNext (click)="completeStep1()">Next</button>
    </div>
  </mat-step>

  <!-- Step 2 -->
  <mat-step [completed]="step2Completed">
    <ng-template matStepLabel>
      <div class="step-label">
        <mat-icon *ngIf="step2Completed">check_circle</mat-icon>
        <span *ngIf="!step2Completed && stepper.selectedIndex === 1" class="active-icon"></span>
        <span *ngIf="!step2Completed && stepper.selectedIndex !== 1" class="inactive-icon"></span>
        Step 2
      </div>
    </ng-template>
    <div>
      <h3>Step 2: Select FAFs to Update</h3>
      <button mat-button matStepperPrevious>Back</button>
      <button mat-button matStepperNext (click)="completeStep2()">Next</button>
    </div>
  </mat-step>

  <!-- Step 3 -->
  <mat-step>
    <ng-template matStepLabel>
      <div class="step-label">
        <mat-icon *ngIf="stepper.selectedIndex > 2">check_circle</mat-icon>
        <span *ngIf="stepper.selectedIndex === 2" class="active-icon"></span>
        <span *ngIf="stepper.selectedIndex !== 2" class="inactive-icon"></span>
        Step 3
      </div>
    </ng-template>
    <div>
      <h3>Step 3: Review and Confirm</h3>
      <button mat-button matStepperPrevious>Back</button>
      <button mat-button (click)="finishStepper()">Finish</button>
    </div>
  </mat-step>
</mat-horizontal-stepper>
```

---

### 2. Add CSS for Icon Styling
Add custom styles to visually differentiate between active, completed, and future steps.

#### CSS:
```css
.step-label {
  display: flex;
  align-items: center;
  gap: 8px;
}

mat-icon {
  color: green;
  font-size: 24px;
}

.active-icon {
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background-color: red; /* Color for the current step */
}

.inactive-icon {
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background-color: gray; /* Color for future steps */
}
```

---

### 3. Add Logic in Component
Update the logic for step completion in your component.

#### Component Logic:
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-stepper',
  templateUrl: './stepper.component.html',
  styleUrls: ['./stepper.component.css']
})
export class StepperComponent {
  step1Completed = false;
  step2Completed = false;

  completeStep1() {
    this.step1Completed = true;
  }

  completeStep2() {
    this.step2Completed = true;
  }

  finishStepper() {
    console.log('Stepper finished');
  }
}
```

---

### Explanation:
1. **Icons Logic:**
   - The `mat-icon` is displayed for completed steps using `check_circle`.
   - For the current step, a red circle (`active-icon`) is used.
   - For future steps, a gray circle (`inactive-icon`) is displayed.

2. **Styling:**
   - Custom CSS ensures the icons and circles look similar to the screenshot provided.

This approach ensures your stepper visually aligns with the example in your images. Let me know if you have further questions!
