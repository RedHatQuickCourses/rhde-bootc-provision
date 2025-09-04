Select the best answer to the following questions:

---
Q1: What is the primary relationship between Red Hat Device Edge (RHDE) and Red Hat Enterprise Linux (RHEL)?

A: RHDE is a lightweight, stripped-down version of RHEL designed exclusively for small ARM-based computers.
Incorrect: Red Hat Device Edge is not a different edition or subset of RHEL; it includes the full feature set of RHEL and is supported on various CPU architectures, not just ARM.

A: RHDE is a subscription bundle that includes the full feature set of RHEL, but with pricing and support tailored for edge devices.
Correct: RHDE is a software and support subscription that bundles RHEL, MicroShift, and Ansible Automation Platform, providing the full RHEL feature set with a pricing model aligned to the characteristics of edge devices rather than large servers.

A: RHDE is a completely separate operating system from RHEL, built from the ground up for edge computing.
Incorrect: Red Hat Device Edge is not a separate operating system; it uses RHEL as its foundation, ensuring that the same OS can be used in both edge and data center scenarios for increased standardization.

A: RHEL is an optional component of an RHDE subscription, which primarily focuses on MicroShift and Ansible.
Incorrect: RHEL is one of the three core components of the Red Hat Device Edge subscription bundle, not an optional one.

---
Q2: What is the main advantage of updating a system using image mode compared to the traditional package mode?

A: Image mode updates are smaller and faster because they only contain the changed files, unlike package mode which replaces entire RPMs.
Incorrect: Bootc container images for updates are complete system images and are considerably larger than individual packages; the advantage lies in reliability, not size.

A: Image mode allows for live kernel patching without a reboot, a feature not available in package mode.
Incorrect: The documentation does not state that image mode enables live kernel patching; its primary benefit is the transactional and reliable nature of its updates. IMPROVE: Research if live kernel patching applies to image mode as well, and say so.

A: Image mode updates are transactional, applying a single system image at once, which prevents the system from being left in an unstable, partially updated state if the process fails.
Correct: Image mode updates are performed from a single system image in a transactional operation. If an update fails, the system can continue using the previous image, avoiding the intermediate, inconsistent states that can occur with package mode failures.

A: Image mode systems do not require a package manager like DNF, which significantly reduces their disk footprint compared to package mode systems.
Incorrect: Bootc container images are built using a package manager like DNF to install RPMs, and the package manager is present within the image; the mode of operation is different, but the tools are still used in the image-building process.

---
Q3: What essential component is found in a bootc container image that is typically absent from a standard application container image?

A: A bootc container image includes a Linux kernel, an initial RAM disk (initrd), and a boot loader.
Correct: A bootc container image is designed to provide a complete system and therefore includes components not found in typical application containers, such as a Linux kernel, initrd, and a boot loader like grub.

A: A bootc container image includes the `systemd` init system, which is never present in application containers.
Incorrect: While bootc images always contain `systemd`, some application containers also include `systemd` to manage multiple services, so its presence is not a unique differentiator.

A: A bootc container image includes application source code, whereas application containers only include compiled binaries.
Incorrect: Neither bootc images nor application images typically contain source code; they both contain compiled software and binaries installed from packages.

A: A bootc container image includes a container engine like Podman to manage other containers on the device.
Incorrect: A bootc container image does not necessarily include a container engine; it contains the operating system itself. A container engine can be added, but it is not a fundamental component that distinguishes it from an application container.

---
Q4: When testing a bootc container image by running it with Podman, which of the following configurations can you NOT effectively validate?

A: The successful installation and enabling of a system service like the Apache Web Server (`httpd`).
Incorrect: You can verify that a user-space service like `httpd` is installed and running inside the container, as this does not depend on the host's kernel settings.

A: The presence and content of application files copied into a directory like `/var/www/html`.
Incorrect: You can easily verify the existence and content of files inside the container's filesystem by starting a shell within the container or inspecting its layers.

A: The existence of custom configuration files placed in the `/etc` directory.
Incorrect: Configuration files are part of the container's filesystem and their presence can be confirmed by running the container and inspecting the relevant paths.

A: Kernel boot arguments specified in `/usr/lib/bootc/kargs.d` that are intended to be applied by the bootloader.
Correct: A container engine like Podman uses the host system's running kernel and ignores the kernel, bootloader, and associated system settings within the bootc image. Therefore, you cannot verify that kernel arguments or other system-level settings are correctly applied without installing the image in a VM.

---
Q5: What is the most significant difference in the containerfile when building a bootc container image versus a typical application container image?

A: It must include a `LABEL containers.bootc="1"` instruction to be recognized as a bootc image.
Incorrect: This label is a convention used to identify bootc images, but it is typically inherited from the base image rather than being explicitly added by the user in a derived `Containerfile`.

A: The `FROM` instruction specifies a base image that contains a full operating system, including a kernel, such as `rhel-bootc`.
Correct: The defining characteristic of a `Containerfile` for a bootc image is that its `FROM` directive uses a bootc container image as its base, which provides all the necessary system-level components, instead of a standard application base image like UBI.

A: The `RUN` instructions must use `firewall-offline-cmd` instead of `firewall-cmd` to configure the firewall.
Incorrect: This is an example of a specific command needed to configure a system service without a running daemon during the build, but it is a detail and not the most fundamental difference, which is the choice of the base image.

A: It cannot use an `ENTRYPOINT` or `CMD` instruction, as the system is booted by `systemd` instead.
Incorrect: While it is true that these images do not typically define an `ENTRYPOINT` or `CMD` for system use, the primary distinction is the base image from which all system capabilities are derived.

---
Q6: How does the filesystem layout of a running image mode system handle application data and system configurations?

A: The entire filesystem, including `/etc` and `/var`, is immutable, and all changes are lost upon reboot.
Incorrect: Describing the system as "immutable" is imprecise; the `/etc` and `/var` directories must be mutable to allow for configuration and data storage.

A: Only the `/opt` directory is writable for installing third-party applications, while the rest of the filesystem is read-only.
Incorrect: The root filesystem and its subdirectories like `/usr` and `/opt` are read-only, but `/etc` and `/var` are specifically designated as read-write.

A: The `/` directory is read-only, but `/etc` and `/var` are writable to allow for day-2 configuration changes and storage of application data.
Correct: Image mode systems feature a read-only root filesystem for immutability, but `/etc` is read-write for system configuration, and `/var` is read-write for application data, logs, and other variable content.

A: The `/etc` directory is read-only as part of the image, while `/var` is a symbolic link to a temporary in-memory filesystem.
Incorrect: The `/etc` directory is explicitly read-write to allow for day-2 customizations. Some directories like `/home` are symlinked into `/var`, but `/var` itself is persistent storage, not a temporary filesystem.

---
Q7: A web application in a bootc image works when tested with `podman run` but fails on a VM due to an SELinux "permission denied" error. What is the most likely cause of this discrepancy?

A: The bootc image is missing the `selinux-policy-targeted` package, which Podman's host machine provided automatically during the container test.
Incorrect: A bootc image based on RHEL will contain the necessary SELinux policy packages; the issue arises from how the policy is applied, not its absence.

A: The VM's kernel is a different version than the host's kernel that Podman used, causing an incompatibility with the SELinux policy modules.
Incorrect: While kernel differences can exist, the more direct cause is the difference in SELinux enforcement models between a container runtime and a fully booted system, not a kernel version mismatch.

A: The container engine runs the image with a permissive container-specific SELinux context, while the VM enforces the full system's targeted policy, revealing that files had the wrong context labels.
Correct: Application containers run within a single per-container context, which can mask underlying file labeling issues. When the same image is booted in a VM, the standard targeted SELinux policy is enforced, and incorrect file context labels (e.g., `default_t` instead of `httpd_sys_content_t`) will cause access denials.

A: Podman automatically disables SELinux for all containers by default, whereas the VM has it enabled in enforcing mode.
Incorrect: Podman does not disable SELinux; it integrates with it to provide container isolation. The discrepancy comes from the different type of SELinux context being applied.

---
Q8: How must you provision a RHEL system in image mode when using the standard RHEL installation media and the Anaconda installer?

A: You must use the `bootc image builder` tool to create a custom ISO, as the standard RHEL media does not support image mode.
Incorrect: While using `bootc image builder` is an option, the standard RHEL installation media can be used to install an image mode system, provided you use a kickstart script.

A: You can select "Image Mode Installation" from the main interactive menu and provide the URL to the container registry.
Incorrect: The interactive mode of Anaconda does not currently have an option to select a bootc container image as its installation source; a kickstart script is mandatory.

A: You must first install a minimal package mode system and then run the `bootc install` command to convert it to image mode.
Incorrect: This describes an alternative installation method, but it is not the procedure used when starting from the standard RHEL installation media with Anaconda.

A: You must provide a kickstart script that specifies the bootc container image as the installation source using the `ostreecontainer` command.
Correct: To install an image mode system using Anaconda, you must provide a kickstart script. This script uses the `ostreecontainer` command to define the bootc container image that will be used as the source for the installation.

---
Q9: In an image mode system, how are configuration files located in `/etc` handled during a system update from a new bootc image?

A: The update process ignores the `/etc` directory entirely, requiring all configuration changes to be applied manually after the update.
Incorrect: The contents of `/etc` are not ignored; they are actively managed and merged during an update to balance new defaults with local customizations.

A: All files in the `/etc` directory are completely overwritten with the versions from the new bootc image, erasing any local modifications.
Incorrect: Overwriting `/etc` would erase all day-2 customizations, which contradicts the design. Instead, a merge process is used to preserve local changes.

A: The update fails if it detects any local modifications in `/etc`, forcing the administrator to revert them before proceeding.
Incorrect: The system is designed to handle local modifications in `/etc` during an update through a merge process, not by failing the update.

A: Configuration files from the new image are merged with the existing files on the system, preserving local day-2 changes while applying updates.
Correct: During an update, files from `/etc` are merged between the current state on the system and the state in the new image. This allows the new image to provide updated default configurations without overwriting changes made by administrators on the live system.

---
Q10: When managing bootc container images in a CI/CD pipeline, what is the recommended practice for using fixed and floating tags?

A: Only the `latest` floating tag should be used to simplify deployment, and older images should be identified by their SHA256 digest.
Incorrect: Relying solely on the `latest` tag and digests is not a robust strategy for managing different versions and testing stages; a more structured tagging scheme is recommended.

A: Fixed tags should be used for development images, while floating tags are exclusively used for production-ready images.
Incorrect: This is too simplistic; floating tags can exist for different stages (e.g., latest stable, latest testing), and fixed tags are crucial for identifying specific builds at all stages, including production.

A: Each build is given a unique, fixed tag (e.g., `v1.2-3247`), and a floating tag (e.g., `v1.2`) is only pointed to a build after it has passed all automated tests.
Correct: It is common practice for automated build systems to assign a unique, fixed tag (like a build number or timestamp) to every image. A floating tag, representing a release line like `v1.2`, is then updated to point to the fixed tag of a specific build only after it has been validated by the CI pipeline.

A: All images should be pushed with a floating tag, and the CI system should delete and replace the tag for each new build to save registry space.
Incorrect: Constantly replacing a single floating tag makes it difficult to track versions, test specific builds, or roll back to a previously known-good version. It is better to use a combination of fixed and floating tags.