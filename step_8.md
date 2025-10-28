

### Step 8
Step 8: Implementation step 8 for Restart VM
content='- name: Wait for the VM to become reachable via SSH after restart\n  ansible.builtin.wait_for_connection:\n    timeout: 300 # Wait up to 5 minutes for the VM to become reachable\n    delay: 10    # Check every 10 seconds for connectivity' usage=None model='gemini-2.5-flash' finish_reason='1'


### Step 8
Step 8: Implementation step 8 for Restart VM
content='- name: Ensure the VM is powered off before restart\n  ansible.builtin.command: "virsh shutdown {{ vm_name }}"\n  register: shutdown_result\n  ignore_errors: yes\n\n- name: Wait for the VM to be powered off\n  ansible.builtin.wait_for:\n    timeout: 300\n    state: stopped\n    delay: 10\n    port: 22\n    host: "{{ vm_ip }}"\n  when: shutdown_result.rc == 0\n\n- name: Restart the VM\n  ansible.builtin.command: "virsh start {{ vm_name }}"\n  register: start_result\n\n- name: Wait for the VM to be up and running\n  ansible.builtin.wait_for:\n    timeout: 300\n    state: started\n    delay: 10\n    port: 22\n    host: "{{ vm_ip }}"\n  when: start_result.rc == 0\n\n- name: Verify the VM is running\n  ansible.builtin.command: "virsh list --state running"\n  register: vm_status\n\n- name: Fail if the VM is not running\n  ansible.builtin.fail:\n    msg: "The VM {{ vm_name }} failed to start."\n  when: "\'{{ vm_name }}\' not in vm_status.stdout"' usage={'prompt_tokens': 78, 'completion_tokens': 265, 'total_tokens': 343} model='gpt-4o-mini-2024-07-18' finish_reason='stop'


### Step 8
Step 8: Implementation step 8 for Restart VM
content='' usage=None


### Step 8
Step 8: Implementation step 8 for Restart VM
content="- name: Restart the virtual machine\n  ansible.builtin.command: shutdown -r now\n  when: ansible_virtualization_type == 'kvm'"


### Step 8
Step 8: Implementation step 8 for Restart VM
content='- name: Restart the virtual machine\n  ansible.builtin.shell: |\n    virsh shutdown {{ vm_name }} || true\n    virsh start {{ vm_name }}\n  register: vm_restart\n  ignore_errors: yes\n\n- name: Wait for the VM to be up\n  ansible.builtin.wait_for:\n    port: 22\n    delay: 10\n    timeout: 300\n    state: started\n    host: "{{ vm_ip }}"' usage={'prompt_tokens': 74, 'completion_tokens': 96, 'total_tokens': 170} model='gpt-4o-mini-2024-07-18' finish_reason='stop'
