---
description: "Learn more about: System Trailers"
title: "System Trailers"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""
ms.suite: ""
ms.topic: "article"
---
# System Trailers
System trailers convey additional or special details about the SWIFT message. If any of the first three system trailers are present, they occur in the following order. The remaining system trailers can occur in any order.  
  
|Trailer code|Name|  
|------------------|----------|  
|**CHK**|Checksum|  
|**SYS**|System Originated Message|  
|**TNG**|Training|  
|**PDM**|Possible Duplicate Message|  
|**DLM**|Delayed Message|  
|**MRF**|Message Reference|  
  
- **System Originated Message (SYS) Trailer.** The system message or service message, which is generated by a system PLT, has a SYS trailer. All solicited system messages with a Service Identifier of 01, contain the MIR of the request, and may contain the time.  
  
   The following code is an example of the SYS trailer format:  
  
  ```  
  {SYS:[<time><mir>]}  
  ```  
  
- **Test & Training Message (TNG) Trailer.** The TNG trailer is mandatory for FIN and GPA messages (with a Service Identifier of 01) sent by, or delivered to, a Test and Training Logical Terminal (LT). This trailer has a tag only, and no value.  
  
   The following code is an example of the TNG trailer format:  
  
  ```  
  {TNG:}  
  ```  
  
- **Possible Duplicate Emission (PDE) Trailer.** The destination of the message uses the PDE trailer. It only applies to FIN user-to-user messages (with a Service Identifier of 01) and message categories reserved for banking messages. The system may contain multiple PDEs. The system does not verify the order nor restrict the number (except for maximum message length).  
  
   The system accepts correctly formatted PDE trailers applied to user-to-system messages, but does not process them. This means that the system does not check to see if the original message exists. Therefore, the system may process a retrieval request sent with a PDE trailer twice—if the system received the original message.  
  
   The following code is an example of the PDE trailer format:  
  
  ```  
  {PDE:[<time><mir>]}  
  where <time><mir> refers to the emission of the previous possible issue  
  ```  
  
- **Delayed Message (DLM) Trailer.** The DLM trailer is added to all FIN user-to-user output messages that have exceeded their obsolescence period. If this trailer appears in GPA or FIN system messages, you can ignore it. This trailer has a tag only, and no value.  
  
   The obsolescence period is as follows:  
  
  - U = 15 minutes  
  
  - N = 100 minutes  
  
    The following code is an example of the DLM trailer format:  
  
  ```  
  {DLM:}  
  ```  
  
- **Possible Duplicate Message (PDM) Trailer.** The PDM trailer is added by the system to any output message (GPA and FIN with a Service Identifier of 01) being resent because a prior delivery may not be valid. If a system PLT receives a report request with a PDM trailer, the response has a plain PDM (without the optional delivery reference). Other PDMs may be added because of unsuccessful delivery attempts to the user.  
  
   The following code is an example of the PDM trailer format:  
  
  ```  
  {PDM:[<time><mor>]}  
  where <time> and the Message Output Reference <mor> are that of the previous attempt  
  ```  
  
- **Message Reference (MRF) Trailer.** The MRF trailer specifies the message reference of the original user message in MT 096 FIN Copy to Central Institution Messages.  
  
   The following code is an example of the MRF trailer format:  
  
  ```  
  {MRF:<date><full-time><mir>}  
  where <mir> is that of the original user message whose fields are copied in the MT 096 FIN  
  Copy to Central Institution Message  
  ```  
  
  > [!NOTE]
  >  The MRF trailer is specific to FIN Copy and is automatically generated in the MT 096 FIN Copy to Central Institution Message. You can only use this trailer in field 109 of the MT 096 FIN Copy to Central Institution Message to identify the MT 096 to which the MT 097 is a response. The format of the MRF is subject to change.  
  
## See Also  
 [Working with Schemas](../../adapters-and-accelerators/accelerator-swift/working-with-schemas.md)
