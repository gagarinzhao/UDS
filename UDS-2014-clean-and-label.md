---
title: "UDS 2014"
author: "Gagarin Zhao"
date: "8/10/2020"
output: github_document
---


loading knitter and packages:

```{r setup}
knitr::opts_chunk$set(echo = TRUE)
library(tidyverse)
library(labelled)
library(openxlsx)
```

## R markdown

This is when I imported and cleaned my data. I labeled the relevant variables.

```{r import and cleaning center info/table5}
uds2014centerinfo = 
  readxl::read_excel(".\\UDS2014DataDumpLA21Aug2017.xlsx", sheet = "HealthCenterInfo") %>% 
  mutate(HealthCenterName = str_to_title(HealthCenterName), HealthCenterStreetAddress = str_to_title(HealthCenterStreetAddress)) #Fixed all cap center names and street addresses


uds2014table5 = 
  readxl::read_excel(".\\UDS2014DataDumpLA21Aug2017.xlsx", sheet = "Table5") %>% 
  select(-GrantNumber)

var_label(uds2014table5) = list(T5_L1_Ca = "Family Practitioner FTE",
                                T5_L1_Cb = "Family Practioner Visits",
                                T5_L2_Ca = "Gen Practitioner FTE",
                                T5_L2_Cb = "Gen Practitioner Visits",
                                T5_L3_Ca = "Internist FTE",
                                T5_L3_Cb = "Internist Visits",
                                T5_L4_Ca = "OBGYN FTE",
                                T5_L4_Cb = "OBGYN Visits",
                                T5_L5_Ca = "Ped FTE",
                                T5_L5_Cb = "Ped Visits",
                                T5_L7_Ca = "Other Specialty FTE",
                                T5_L7_Cb = "Other Specialty Visits",
                                T5_L8_Ca = "Total Physician FTE",
                                T5_L8_Cb = "Total Physician Visits",
                                T5_L9a_Ca = "NP FTE",
                                T5_L9a_Cb = "NP Visits",
                                T5_L9b_Ca = "PA FTE",
                                T5_L9b_Cb = "PA Visits",
                                T5_L10_Ca = "CNM FTE",
                                T5_L10_Cb = "CNM Visits",
                                T5_L10a_Ca = "Total NPs, PAs, CNMs FTE",
                                T5_L10a_Cb = "Total NPs, PAs, CNMs Visits",
                                T5_L11_Ca = "Nurses FTE",
                                T5_L11_Cb = "Nurses Visits",
                                T5_L12_Ca = "Other Med Personnel FTE",
                                T5_L13_Ca = "Lab Personnel FTE",
                                T5_L14_Ca = "Xray Personnel FTE",
                                T5_L15_Ca = "Total Medical FTE",
                                T5_L15_Cb = "Total Medical Visits",
                                T5_L15_Cc = "Total Medical Patients",
                                T5_L16_Ca = "Dentist FTE",
                                T5_L16_Cb = "Dentist Visits",
                                T5_L17_Ca = "Dental Hygienist FTE",
                                T5_L17_Cb = "Dental Hygienist Visits",
                                T5_L17a_Ca = "Dental Therapist FTE",
                                T5_L17a_Cb = "Dental Therapist Visits",
                                T5_L18_Ca = "Other Dental Personnel FTE",
                                T5_L19_Ca = "Total Dental Services FTE",
                                T5_L19_Cb = "Total Dental Services Visits",
                                T5_L19_Cc = "Total Dental Services Patients",
                                T5_L20_Ca = "Total Mental Health FTE",
                                T5_L20_Cb = "Total Mental Health Visits",
                                T5_L20_Cc = "Total Mental Health Patients",
                                T5_L21_Ca = "Total SUD FTE",
                                T5_L21_Cb = "Total SUD Visits",
                                T5_L21_Cc = "Total SUD Patients",
                                T5_L22_Ca = "Other Professional Services FTE",
                                T5_L22_Cb = "Other Professional Services Visits",
                                T5_L22_Cc = "Other Professional Services Patients",
                                T5_L22a_Ca = "Opthalmologist FTE",
                                T5_L22a_Cb = "Opthalmologist Visits",
                                T5_L22b_Ca = "Optometrist FTE",
                                T5_L22b_Cb = "Optometrist Visits",
                                T5_L22c_Ca = "Other Vision Care FTE",
                                T5_L22d_Ca = "Total Vision Services FTE",
                                T5_L22d_Cb = "Total Vision Services Visits",
                                T5_L22d_Cc = "Total Vision Services Patients",
                                T5_L23_Ca = "Pharmacy Personnel FTE",
                                T5_L24_Ca = "Case Managers FTE",
                                T5_L24_Cb = "Case Managers Visits",
                                T5_L25_Ca = "Patient/Community Ed Spec FTE",
                                T5_L25_Cb = "Patient/Community Ed Spec Visits",
                                T5_L26_Ca = "Outreach Workers FTE",
                                T5_L27_Ca = "Transportation FTE",
                                T5_L27a_Ca = "Eligibility Assistance FTE",
                                T5_L27b_Ca = "Interpretation FTE",
                                T5_L27c_Ca = "Community Health Worker FTE",
                                T5_L28_Ca = "Other Enabling SErvices FTE",
                                T5_L29_Ca = "Total Enabling Services FTE",
                                T5_L29_Cb = "Total Enabling Services Visits",
                                T5_L29_Cc = "Total Enabling Services Patients",
                                T5_L29a_Ca = "Other Programs FTE",
                                T5_L29b_Ca = "Quality Improvement FTE",
                                T5_L30a_Ca = "Management and Support FTE",
                                T5_L30b_Ca = "Fiscal and Billing FTE",
                                T5_L30c_Ca = "IT FTE",
                                T5_L31_Ca = "Facility Staff FTE",
                                T5_L32_Ca = "Patient Support FTE",
                                T5_L33_Ca = "Total Facility/Non-Clinical Support Staff FTE",
                                T5_L34_Ca = "Grand Total FTE",
                                T5_L34_Cb = "Grand Total Visits"
                                ) 
```

Loaded in table 5, removed grant number column, kept only part time and full time staff values.

```{r import and cleaning table 5a}
uds2014table5a = 
  readxl::read_excel(".\\UDS2014DataDumpLA21Aug2017.xlsx", sheet = "Table5A") %>% 
  select(-GrantNumber)

uds2014table5a = uds2014table5a[,!grepl("Cc$|Cd$",names(uds2014table5a))] #removing locum and on-call staff, only keeping columns a and b

var_label(uds2014table5a) = list(T5A_L1_Ca = "FT/PT Family Physicians Persons",
                                T5A_L1_Cb = "FT/PT Family Physicians Months",
                                T5A_L2_Ca = "FT/PT Gen Prac Persons",
                                T5A_L2_Cb = "FT/PT Gen Prac Internist Months",
                                T5A_L3_Ca = "FT/PT Internists Persons",
                                T5A_L3_Cb = "FT/PT Internists Months",
                                T5A_L4_Ca = "FT/PT OBGYN Persons",
                                T5A_L4_Cb = "FT/PT OBGYN Months",
                                T5A_L5_Ca = "FT/PT Ped Persons",
                                T5A_L5_Cb = "FT/PT Ped Months",
                                T5A_L7_Ca = "FT/PT Other Spec Phys Persons",
                                T5A_L7_Cb = "FT/PT Other Spec Phys Months",
                                T5A_L9a_Ca = "FT/PT NP Persons",
                                T5A_L9a_Cb = "FT/PT NP Months",
                                T5A_L9b_Ca = "FT/PT PA Persons",
                                T5A_L9b_Cb = "FT/PT PA Months",
                                T5A_L10_Ca = "FT/PT CNM Persons",
                                T5A_L10_Cb = "FT/PT CNM Months",
                                T5A_L11_Ca = "FT/PT Nurses Persons",
                                T5A_L11_Cb = "FT/PT Nurses Months",
                                T5A_L16_Ca = "FT/PT Dentists Persons",
                                T5A_L16_Cb = "FT/PT Dentists Months",
                                T5A_L17_Ca = "FT/PT Dental Hygienists Persons",
                                T5A_L17_Cb = "FT/PT Dental Hygienists Months",
                                T5A_L17a_Ca = "FT/PT Dental Therapists Persons",
                                T5A_L17a_Cb = "FT/PT Dental Therapists Months",
                                T5A_L20a_Ca = "FT/PT Psychiatrists Persons",
                                T5A_L20a_Cb = "FT/PT Psychiatrists Months",
                                T5A_L20a1_Ca = "FT/PT LC Psychologists Persons",
                                T5A_L20a1_Cb = "FT/PT LC Psychologists Months",
                                T5A_L20a2_Ca = "FT/PT LC Social Workers Persons",
                                T5A_L20a2_Cb = "FT/PT LC SOcial Workers Months",
                                T5A_L20b_Ca = "FT/PT Other Licensed Mental Health Persons",
                                T5A_L20b_Cb = "FT/PT Other Licensed Mental Health Months",
                                T5A_L22a_Ca = "FT/PT Opthalmologist Persons",
                                T5A_L22a_Cb = "FT/PT Opthalmologist Months",
                                T5A_L22b_Ca = "FT/PT Optometrist Persons",
                                T5A_L22b_Cb = "FT/PT Optometrist Months",
                                T5A_L30a1_Ca = "FT/PT CEO Persons",
                                T5A_L30a1_Cb = "FT/PT CEO Months",
                                T5A_L30a2_Ca = "FT/PT CMO Persons",
                                T5A_L30a2_Cb = "FT/PT CMO Months",
                                T5A_L30a3_Ca = "FT/PT CFO Persons",
                                T5A_L30a3_Cb = "FT/PT CFO Months",
                                T5A_L30a4_Ca = "FT/PT CIO Persons",
                                T5A_L30a4_Cb = "FT/PT CIO Months"
                                )
```


```{r import and cleaning table 6a}
uds2014table6a = 
  readxl::read_excel(".\\UDS2014DataDumpLA21Aug2017.xlsx", sheet = "Table6A") %>% 
  select(-GrantNumber)

var_label(uds2014table6a) = list(T6a_L1and2_Ca = "Symp/Asymp HIV # Visits",
                                 T6a_L1and2_Cb = "Symp/Asymp HIV # Patients",
                                 T6a_L3_Ca = "TB # Visits",
                                 T6a_L3_Cb = "TB # Patients",
                                 T6a_L4a_Ca = "Hep B # Visits",
                                 T6a_L4a_Cb = "Hep B # Patients",
                                 T6a_L4b_Ca = "Hep C # Visits",
                                 T6a_L4b_Cb = "Hep C # Patients",
                                 T6a_L5_Ca = "Asthma # Visits",
                                 T6a_L5_Cb = "Asthma # Patients",
                                 T6a_L6_Ca = "Chronic lower resp dis # Visits",
                                 T6a_L6_Cb = "Chronic lower resp dis # Patients",
                                 T6a_L7_Ca = "Abn Breast # Visits",
                                 T6a_L7_Cb = "Abn Breast # Patients",
                                 T6a_L8_Ca = "Abn Cervical # Visits",
                                 T6a_L8_Cb = "Abn Cervical # Patients",
                                 T6a_L9_Ca = "Diabetes mel # Visits",
                                 T6a_L9_Cb = "Diabetes mel # Patients",
                                 T6a_L10_Ca = "Heart Disease # Visits",
                                 T6a_L10_Cb = "Heart Disease # Patients",
                                 T6a_L11_Ca = "Hypertension # Visits",
                                 T6a_L11_Cb = "Hypertension # Patients",
                                 T6a_L12_Ca = "Contact derm, eczema # Visits",
                                 T6a_L12_Cb = "Contact derm, eczema # Patients",
                                 T6a_L13_Ca = "Dehydration # Visits",
                                 T6a_L13_Cb = "Dehydration # Patients",
                                 T6a_L14_Ca = "Exp to heat/cold # Visits",
                                 T6a_L14_Cb = "Exp to heat/cold # Patients",
                                 T6a_L14a_Ca = "Overweight/obesity # Visits",
                                 T6a_L14a_Cb = "Overweight/obesity # Patients",
                                 T6a_L15_Ca = "Media/Eustachian tube # Visits",
                                 T6a_L15_Cb = "Media/Eustachian tube # Patients",
                                 T6a_L16_Ca = "Perinatal # Visits",
                                 T6a_L16_Cb = "Perinatal # Patients",
                                 T6a_L17_Ca = "Lack of development # Visits",
                                 T6a_L17_Cb = "Lack of development # Patients",
                                 T6a_L18_Ca = "Alcohol # Visits",
                                 T6a_L18_Cb = "Alcohol # Patients",
                                 T6a_L19_Ca = "Substance excl tob # Visits",
                                 T6a_L19_Cb = "Substance excl tob # Patients",
                                 T6a_L19a_Ca = "Tobacco # Visits",
                                 T6a_L19a_Cb = "Tobacco # Patients",
                                 T6a_L20a_Ca = "Depression # Visits",
                                 T6a_L20a_Cb = "Depression # Patients",
                                 T6a_L20b_Ca = "Anxiety, PTSD # Visits",
                                 T6a_L20b_Cb = "Anxiety, PTSD # Patients",
                                 T6a_L20c_Ca = "Attention/Disruptive # Visits",
                                 T6a_L20c_Cb = "Attention/Disruptive # Patients",
                                 T6a_L20d_Ca = "Other mental excl drug/alc # Visits",
                                 T6a_L20d_Cb = "Other mental excl drug/al # Patients",
                                 T6a_L21_Ca = "HIV Test # Visits",
                                 T6a_L21_Cb = "HIV Test # Patients",
                                 T6a_L21a_Ca = "Hep B Test # Visits",
                                 T6a_L21a_Cb = "Hep B Test # Patients",
                                 T6a_L21b_Ca = "Hep C Test # Visits",
                                 T6a_L21b_Cb = "Hep C Test # Patients",
                                 T6a_L22_Ca = "Mammogram # Visits",
                                 T6a_L22_Cb = "Mammogram # Patients",
                                 T6a_L23_Ca = "Pap Test # Visits",
                                 T6a_L23_Cb = "Pap Test # Patients",
                                 T6a_L24_Ca = "Select immu # Visits",
                                 T6a_L24_Cb = "Select immu # Patients",
                                 T6a_L24a_Ca = "Seasonal flu shot # Visits",
                                 T6a_L24a_Cb = "Seasonal flu shot # Patients",
                                 T6a_L25_Ca = "Contraceptive # Visits",
                                 T6a_L25_Cb = "Contraceptive # Patients",
                                 T6a_L26_Ca = "Health supervision infant # Visits",
                                 T6a_L26_Cb = "Health supervision infant # Patients",
                                 T6a_L26a_Ca = "Childhood lead testing screen # Visits",
                                 T6a_L26a_Cb = "Childhood lead testing screen # Patients",
                                 T6a_L26b_Ca = "SBIRT # Visits",
                                 T6a_L26b_Cb = "SBIRT # Patients",
                                 T6a_L26c_Ca = "Smoke/tob Counseling # Visits",
                                 T6a_L26c_Cb = "Smoke/tob Counseling # Patients",
                                 T6a_L26d_Ca = "Comp/interm eye exam # Visits",
                                 T6a_L26d_Cb = "Comp/interm eye exam # Patients",
                                 T6a_L27_Ca = "Dent Emergency Services # Visits",
                                 T6a_L27_Cb = "Dent Emergency Services # Patients",
                                 T6a_L28_Ca = "Oral Exams # Visits",
                                 T6a_L28_Cb = "Oral Exams # Patients",
                                 T6a_L29_Ca = "Dent Prophylaxis # Visits",
                                 T6a_L29_Cb = "Dent Prophylaxis # Patients",
                                 T6a_L30_Ca = "Dent Sealants # Visits",
                                 T6a_L30_Cb = "Dent Sealants # Patients",
                                 T6a_L31_Ca = "Dent Fluoride # Visits",
                                 T6a_L31_Cb = "Dent Fluoride # Patients",
                                 T6a_L32_Ca = "Dent Restorative # Visits",
                                 T6a_L32_Cb = "Dent Restorative # Patients",
                                 T6a_L33_Ca = "Oral Surg # Visits",
                                 T6a_L33_Cb = "Oral Surg # Patients",
                                 T6a_L34_Ca = "Dent Rehab # Visits",
                                 T6a_L34_Cb = "Dent Rehab # Patients"
                                 )

```

Joined health center info, table 5, 5a by BHCMISID:

```{r join tables}
uds2014info.t5.T5A = full_join(uds2014centerinfo, uds2014table5, by = "BHCMISID") %>% 
  full_join(uds2018table5a, by = "BHCMISID")


```

Export table as an Excel:

```{r export xlsx}
write.xlsx(uds2014info.t5.T5A, "C:\\Users\\GagarinZhao\\Documents\\Work\\UDS\\Data Wrangling\\uds2014info_T5_T5A.xlsx")
```
