To create a stepper like the one shown in the images using Angular Material, you can utilize the `MatStepperModule` provided by Angular Material. Here's how you can implement it:

### 1. Install Angular Material
Make sure Angular Material is installed in your project:
```bash
ng add @angular/material
```

### 2. Import MatStepperModule
In your `app.module.ts`, import the necessary modules:
```typescript
import { MatStepperModule } from '@angular/material/stepper';
import { MatButtonModule } from '@angular/material/button';

@NgModule({
  declarations: [/* Your Components */],
  imports: [
    MatStepperModule,
    MatButtonModule,
    // Other modules
  ],
  bootstrap: [/* Your Main Component */]
})
export class AppModule {}
```

### 3. Add HTML Template for the Stepper
In the component HTML file, use the `<mat-horizontal-stepper>` component:
```html
<mat-horizontal-stepper linear #stepper>
  <!-- Step 1 -->
  <mat-step [completed]="step1Completed" label="Step 1">
    <div>
      <h3>Step 1: Select Fields to Update</h3>
      <button mat-button matStepperNext (click)="completeStep1()">Next</button>
    </div>
  </mat-step>

  <!-- Step 2 -->
  <mat-step label="Step 2">
    <div>
      <h3>Step 2: Select FAFs to Update</h3>
      <button mat-button matStepperPrevious>Back</button>
      <button mat-button matStepperNext (click)="completeStep2()">Next</button>
    </div>
  </mat-step>

  <!-- Step 3 -->
  <mat-step label="Step 3">
    <div>
      <h3>Step 3: Review and Confirm</h3>
      <button mat-button matStepperPrevious>Back</button>
      <button mat-button (click)="finishStepper()">Finish</button>
    </div>
  </mat-step>
</mat-horizontal-stepper>
```

### 4. Add Component Logic
In your component TypeScript file, define the logic for managing step completions:
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-stepper-example',
  templateUrl: './stepper-example.component.html',
  styleUrls: ['./stepper-example.component.css']
})
export class StepperExampleComponent {
  step1Completed = false;

  completeStep1() {
    this.step1Completed = true;
  }

  completeStep2() {
    console.log('Step 2 completed');
  }

  finishStepper() {
    console.log('Stepper completed');
  }
}
```

### 5. Styling (Optional)
You can add custom styles in the component CSS file to match your design:
```css
mat-horizontal-stepper {
  margin: 20px 0;
}

mat-step-header {
  text-transform: none;
  font-size: 14px;
}

h3 {
  margin: 10px 0;
}
```

### 6. Add Angular Material Theme
Ensure your project has an Angular Material theme applied to ensure proper styling.

This will create a functional stepper component similar to the one in your screenshots. You can further customize it with additional styles or behaviors as needed. Let me know if you have any questions!
