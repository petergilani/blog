---
layout: post
title: iOS Shortcut for local OpenAI Whisper Translation/Transcription
---

Recently I've been playing with the open source [Whisper](https://openai.com/research/whisper), and setup an iOS shortcut which I can share a video/audio file to:
[![whisper_flow]({{ site.baseurl }}/images/whisper-flow.jpg)]({{site.baseurl}}/ios-shortcut-openai-whisper)
 - Encodes to an audio file locally on iPad
 - Copies audio file via Files (SMB) to shared folder on local Windows machine
 - SSH script logs into Ubuntu WSL2 SSH server on Windows machine
 - Activates virtual environment and runs Whisper against audio file
 - Displays transcription terminal output on iPad
 - Copies generated text file back to local folder on iPad
 - Opens file in text editor (Textastic) on iPad

This greatly simplifies the workflow, and takes advantage of the local GPU resources I have available, providing a private, free and convenient transcription/translation speech to text service, which I am finding has many use cases.

## Steps
 To initiate a new run, I simply right click on a file, select Share, and select the new shortcut named WHISPER - it then gets to work on the tasks with a loading ring to indicate progress at the top of the screen, and moments later I hear the GPU fans on the other side of the room start to ramp up. Processing takes roughly half the length of the audio being transcribed with a single GPU with the 'large' model. I can crack on with other tasks while waiting and can even run other shortcuts without impacting the existing one running. If for whatever reason the shortcut gets interrupted, then as long as Whisper has started processing, it will continue until complete.

## Security
 The local Windows machine is isolated from the rest of the local network, in its own segment behind a Cisco 1010 firewall running ASA code, and I was able to validate at a basic level with a packet capture and by removing Internet access, that it does not attempt any external DNS or connection requests as it powers through the transcription requests.

 The exception to this is if you specify a previously unused model, which it will then try to first download as part of the task.

## Accuracy
 I'm still evaluating the reliability/accuracy of the different [models](https://huggingface.co/collections/openai/whisper-release-6501bba2cf999715fd953013), but for the moment, prefer 'large-v2' for most tasks:
 ```
 whisper audio.m4a --output_format txt --language English --model large-v2
 ```

 This provides a rich transcription experience, with correct syntax/punctuation/acronyms etc which makes the resulting text significantly more readable compared to the smaller models.

 However for some translation tasks, I have found cases where both large versions have missed entire sentences, which the base model was able to pick up.

## Resources/Alternatives
 Q. Do you really need a powerful GPU to do this?
 A. No and yes..

 I first tested Whisper out on the Raspberry Pi 4B (8GB) which was able to get through files using the tiny model taking ~4 times the length of the file, but a lot longer for larger models. So it works, but isn't really feasible from a time perspective for anything above the base model, at least for my current use cases.
 
 You could use the [OpenAI API](https://platform.openai.com/docs/guides/speech-to-text) and pay the current price of $0.006 per minute, which I understand performs ~x10 faster than my current single GPU speed, however privacy/security concerns would exclude a large number, if not the majority of use cases. There is also a chunk size limit, meaning you have to split up larger files before posting, which is an additional hurdle to get things working.

 While looking into alternatives, I found a 'Show and tell' category in the repo's [Discussions](https://github.com/openai/whisper/discussions/categories/show-and-tell) section and came across [one](https://github.com/openai/whisper/discussions/443) for an iOS app [Hello Transcribe](https://apps.apple.com/za/app/hello-transcribe/id6443919768) which comes with the 'tiny' model for free, and can be switched to the 'base' or 'small' model by buying the pro version, either with a very reasonable one time payment or monthly subscription cost. The privacy notice is impressive stating no data is collected and all processing is done locally on the device. With my iPad Pro M1 1TB, I saw it chew through a 30min file nearly twice as fast as the Windows machine with both using the 'small' model on the same file, 3min30s and 5min30s respectively.
 
 If this app can add the 'large-v2' model then it may completely replace the need for the shortcut and Windows machine, but until then, the shortcut-GPU is the preferred option, providing a private service with the best possible model.

## Wrap up
 I will plan to add more details with some setup steps, commands and screenshots as and when time permits.

 For now, here are some related links:
  - [https://en.wikipedia.org/wiki/Whisper_%2528speech_recognition_system%2529](https://en.wikipedia.org/wiki/Whisper_%2528speech_recognition_system%2529)
  - [https://github.com/openai/whisper](https://github.com/openai/whisper)
  - [https://docs.nvidia.com/cuda/wsl-user-guide/](https://docs.nvidia.com/cuda/wsl-user-guide/)
  - [https://support.apple.com/en-gb/guide/shortcuts/](https://support.apple.com/en-gb/guide/shortcuts/)
  - [https://github.com/m-bain/whisperX](https://github.com/m-bain/whisperX)