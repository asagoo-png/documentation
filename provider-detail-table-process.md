# Provider Detail Table Building Process

This document outlines the process of building the provider detail table, including a pictorial diagram that visualizes the five essential steps involved.

## Process Overview

1. **Analyzing Providers In-Scope**  
   Understand the requirements and identify the providers that need to be included in the table.

2. **Gathering Data**  
   Collect the necessary data for each provider, which may include basic information, NPI numbers, and other relevant identifiers.

3. **Mapping NPI to Source IDs**  
   For each provider, ensure that the NPI numbers are accurately mapped to their corresponding source IDs. This ensures data integrity and usability.

4. **Data Validation**  
   Perform checks to validate the accuracy of the data gathered, identifying any discrepancies or missing information.

5. **Completing the Client-Specific Table**  
   Finalize the table for client use, with all columns filled with the necessary information, ensuring that NPI mappings and source IDs are populated correctly.

## Pictorial Diagram







                       START
                         │
                         ▼
     ┌───────────────────────────────────┐
     │    STEP 1: ANALYZE PROVIDERS      │
     │         IN-SCOPE                  │
     └───────────────────────────────────┘
                         │
     ┌───────────────────┴───────────────────┐
     │                                       │
     ▼                                       ▼
┌──────────────────┐          ┌──────────────────────┐
│ 1.1: SELECT      │          │ 1.2: UNSELECT        │
│ Providers by:     │          │ Older files &        │
│ • ID             │          │ Keep only:            │
│ • bus_nm/npi_    │          │ • New files          │
│   name           │          │                      │
└────────┬─────────┘          └─────────┬────────────┘
         │                               │
         └───────────────┬───────────────┘
                         │
                         ▼
     ┌───────────────────────────────────┐
     │   STEP 2: QUERY NPI REF TABLE     │
     │   & ADD TO CLIENT-SPECIFIC TABLE  │
     └───────────────────────────────────┘
                         │
     ┌───────────────────┴───────────────────────────┐
     │                                               │
     │        Apply Filtering Criteria:             │
     │        ✓ Active ind = TRUE                   │
     │        ✓ NPI type = Organization             │
     │        ✓ Org CCN id ≠ NULL                   │
     │                                               │
     ▼                                               ▼
┌──────────────────┐          ┌──────────────────────┐
│ Hospital Files   │          │ Payer Source IDs     │
│ NPI Details      │          │ (Append same         │
│ Populated        │          │  details)            │
└────────┬─────────┘          └─────────┬────────────┘
         │                               │
         └───────────────┬───────────────┘
                         │
                         ▼
     ┌───────────────────────────────────┐
     │   STEP 3: HANDLE UNMATCHED         │
     │   ENTRIES (Remove Hard Filters)   │
     │   - Be Liberal with Criteria      │
     │   - Retrieve Correct NPI Details  │
     └───────────────┬───────────────────┘
                     │
                     ▼
     ┌───────────────────────────────────┐
     │   STEP 4: MATCH BY ADDRESS        │
     │   (Lone Entries without bus_nm)   │
     │                                   │
     │   • Use hospital file address     │
     │   • Find correct entry match      │
     │   • Prioritize Hospital Files     │
     │     first, then Payer             │
     └───────────────┬───────────────────┘
                     │
                     ▼
     ┌───────────────────────────────────┐
     │   STEP 5: HANDLE PAYER ORPHANS    │
     │                                   │
     │   • Find npi_name in final        │
     │     extract (source_id = payer)   │
     │   • NPI details NOT in table      │
     │     from steps 2-4                │
     │   • Apply Name Grouping/Swapping  │
     │   • Add remaining entries         │
     └───────────────┬───────────────────┘
                     │
                     ▼
     ┌───────────────────────────────────┐
     │   CLIENT-SPECIFIC TABLE COMPLETE  │
     │   ✓ All Provider Details          │
     │   ✓ All NPI Mappings              │
     │   ✓ All Source IDs Populated      │
     └───────────────┬───────────────────┘
                     │
                     ▼
                    END































                    

This diagram illustrates the above steps and helps to provide a visual understanding of the process flow.  
Once completed, the client-specific table should be ready for implementation and use by the designated team.
