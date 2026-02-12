### **Crucial Checklist Before You Buy Second-Hand**

This is the most important part. When buying a used enterprise drive, **you must verify its health**. Do not buy from a seller who will not provide this information.

**Ask the seller for a screenshot of the drive's S.M.A.R.T. data.** (They can get this using a tool like CrystalDiskInfo on Windows or `smartctl` on Linux).

Look for these key attributes in the report:

1. **Percentage Used / Media Wearout Indicator:** This is the most critical value. It tells you how much of the drive's rated lifespan has been consumed. **Look for drives with 10% or less used (i.e., 90%+ life remaining).**
2. **Power On Hours:** Gives you an idea of how long the drive was in service. Lower is generally better, but a drive with high hours and low wear is still a great deal.
3. **Reallocated Sector Count:** This number should be **zero**. If it's anything higher, it means the drive has started to develop bad blocks. Avoid these drives.
4. **Power Cycle Count:** A low number here indicates it was likely in a server that was on 24/7, which is a good sign.

**Pro Tip:** As mentioned before, the best practice is to **buy two identical drives** from the list above. Installing Proxmox on a **ZFS Mirror (RAID 1)** is easy to do during setup and will give you full redundancy, protecting you from a single drive failure and ensuring your server stays online.