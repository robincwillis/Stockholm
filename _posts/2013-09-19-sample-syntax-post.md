---
layout: post
title:  "A Post With Syntax Highlighting"
date:   2013-09-19 09:36:13
tags: Sample
---
~~~~~ruby
#process each packet and add to sequence of checksum is correct
	def process_packet(offset, stream, sequence)
		header = stream.unpack("x#{offset}NNN")
		seq, chk, length = header[0], header[1], header[2]
		data = stream.unpack("x#{offset+12}C#{length}")
		chunks = get_chunks(data.clone, length, 0xAB)

		if(get_checksum(seq, chunks) == chk)
			sequence[seq] = data
		end

		offset += length + 12

		if(offset < stream.length)
			process_packet(offset, stream, sequence)
		else
			sort_sequence(sequence)
		end
	end
~~~~~