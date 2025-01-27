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
