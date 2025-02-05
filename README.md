package com.example.dto;

import lombok.Getter;
import lombok.Setter;
import java.util.Date;

@Getter
@Setter
public class BulkUpdateClientInformationDTO {
    private String clientName;
    private String accountName;
    private String analyst;
    private String platform;
    private String pLCode;
    private String fafId;
    private String lobDescriptor;
    private String lob;
    private String lobSubType;
    private Date contractStartDate;
    private Date contractEndDate;
    private String contractYear;
    private Date effPricingStartDate;
    private Date effPricingEndDate;
    private Boolean earlyPricing;
    private Boolean escalatingPricing;
    private String brandDefinition;
    private String adjudication;
    private Boolean authorizedGenericsAsGenerics;
    private String reconMethod;
    private Boolean reconcileR3OR90;
    private Boolean approved;
    private String peerReviewer;
    private String clientFlags;
    private String manualClientFlags;
    private String timeFrame;
    private String customTimeFrame;
    private String dueDate;
    private String customDueDate;
    private String paymentTermFreq;
    private String paymentTermDueDate;
    private String customPaymentFreq;
    private String customPaymentDueDate;
    private String performanceReportingFrequency;
    private String performanceReportingDueDate;
    private String customPerfReportingFrequency;
    private String customPerfReportingDueDate;
    private String automationFlags;
    private String gmClientFlags;
    private Boolean caremarkSpeciality;
    private Boolean contractLimit;
    private String contractPercent;
    private String contractTimePeriod;
    private Boolean reportingChanges;
    private String reportingRequirements;
}
